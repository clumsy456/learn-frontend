---
layout: default
title: "Day 20：前端测试"
categories: ['进阶', '第四周']
tags: ['测试', 'vitest', 'playwright']
---

#### 学习内容

```bash
# 安装测试工具
pnpm add -D vitest @testing-library/react @testing-library/jest-dom @testing-library/user-event jsdom
```

**1. 单元测试**

```typescript
// utils.test.ts
import { describe, it, expect } from 'vitest';
import { formatCurrency, validateEmail, debounce } from './utils';

describe('formatCurrency', () => {
  it('应该正确格式化金额', () => {
    expect(formatCurrency(1234.5)).toBe('¥1,234.50');
    expect(formatCurrency(0)).toBe('¥0.00');
    expect(formatCurrency(-100)).toBe('-¥100.00');
  });
});

describe('validateEmail', () => {
  it('应该验证有效邮箱', () => {
    expect(validateEmail('test@example.com')).toBe(true);
    expect(validateEmail('invalid')).toBe(false);
    expect(validateEmail('')).toBe(false);
  });
});
```

**2. 组件测试**

```tsx
// Counter.test.tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { describe, it, expect } from 'vitest';
import Counter from './Counter';

describe('Counter', () => {
  it('应该正确渲染初始值', () => {
    render(<Counter initialCount={5} />);
    expect(screen.getByText('5')).toBeInTheDocument();
  });
  
  it('点击 +1 按钮应该增加计数', async () => {
    render(<Counter initialCount={0} />);
    const button = screen.getByRole('button', { name: /increment/i });
    fireEvent.click(button);
    expect(screen.getByText('1')).toBeInTheDocument();
  });
  
  it('应该调用 onChange 回调', async () => {
    const handleChange = vi.fn();
    render(<Counter initialCount={0} onChange={handleChange} />);
    fireEvent.click(screen.getByRole('button', { name: /increment/i }));
    expect(handleChange).toHaveBeenCalledWith(1);
  });
});
```

**3. E2E 测试（Playwright）**

```bash
pnpm add -D @playwright/test
npx playwright install
```

```typescript
// tests/login.spec.ts
import { test, expect } from '@playwright/test';

test('用户登录流程', async ({ page }) => {
  await page.goto('/login');
  
  await page.fill('[name="email"]', 'test@example.com');
  await page.fill('[name="password"]', 'password123');
  await page.click('button[type="submit"]');
  
  await expect(page).toHaveURL('/dashboard');
  await expect(page.getByText('欢迎')).toBeVisible();
});
```

**测试策略（后端工程师视角）**

| 测试类型 | 类比 | 工具 | 覆盖范围 |
|----------|------|------|----------|
| 单元测试 | Go 的 `go test` | Vitest | 工具函数、纯逻辑 |
| 组件测试 | Go 的 handler 测试 | Testing Library | 组件交互 |
| E2E 测试 | Go 的集成测试 | Playwright | 完整用户流程 |
