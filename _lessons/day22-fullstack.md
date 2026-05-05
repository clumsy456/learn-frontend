---
layout: default
title: "Day 22：全栈开发（前后端联调）"
categories: ['进阶', '第四周']
tags: ['全栈', 'api', '联调']
---

#### 学习内容

**1. 前后端通信最佳实践**

```typescript
// services/api.ts — 统一的 API 客户端
const BASE_URL = '/api';

class ApiClient {
  private baseUrl: string;
  
  constructor(baseUrl: string) {
    this.baseUrl = baseUrl;
  }
  
  private async request<T>(
    endpoint: string,
    options: RequestInit = {}
  ): Promise<T> {
    const url = `${this.baseUrl}${endpoint}`;
    const token = localStorage.getItem('token');
    
    const response = await fetch(url, {
      ...options,
      headers: {
        'Content-Type': 'application/json',
        ...(token ? { Authorization: `Bearer ${token}` } : {}),
        ...options.headers,
      },
    });
    
    if (!response.ok) {
      const error = await response.json().catch(() => ({}));
      throw new ApiError(response.status, error.message || '请求失败');
    }
    
    return response.json();
  }
  
  get<T>(endpoint: string) {
    return this.request<T>(endpoint);
  }
  
  post<T>(endpoint: string, data: unknown) {
    return this.request<T>(endpoint, {
      method: 'POST',
      body: JSON.stringify(data),
    });
  }
  
  put<T>(endpoint: string, data: unknown) {
    return this.request<T>(endpoint, {
      method: 'PUT',
      body: JSON.stringify(data),
    });
  }
  
  delete<T>(endpoint: string) {
    return this.request<T>(endpoint, { method: 'DELETE' });
  }
}

class ApiError extends Error {
  constructor(public status: number, message: string) {
    super(message);
  }
}

export const api = new ApiClient(BASE_URL);

// 使用
const users = await api.get<User[]>('/users');
const newUser = await api.post<User>('/users', { name: 'Alice' });
await api.delete(`/users/${id}`);
```

**2. 跨域处理（CORS）**

```go
// Go 后端设置 CORS（后端工程师应该很熟悉）
// 使用 gin 框架
import "github.com/gin-contrib/cors"

r.Use(cors.New(cors.Config{
    AllowOrigins:     []string{"http://localhost:3000"},
    AllowMethods:     []string{"GET", "POST", "PUT", "DELETE", "OPTIONS"},
    AllowHeaders:     []string{"Origin", "Content-Type", "Authorization"},
    AllowCredentials: true,
    MaxAge:           12 * time.Hour,
}))
```

**3. JWT 认证**

```typescript
// 前端 Token 管理
function setToken(token: string) {
  localStorage.setItem('token', token);
}

function getToken(): string | null {
  return localStorage.getItem('token');
}

function clearToken() {
  localStorage.removeItem('token');
}

// 自动刷新 Token
let refreshTimer: NodeJS.Timeout;

function setupTokenRefresh() {
  refreshTimer = setInterval(async () => {
    try {
      const newToken = await api.post('/auth/refresh', {});
      setToken(newToken.token);
    } catch {
      clearToken();
      window.location.href = '/login';
    }
  }, 15 * 60 * 1000); // 每 15 分钟刷新
}

// 请求拦截器（自动添加 Token）
const originalFetch = window.fetch;
window.fetch = async (url, options) => {
  const token = getToken();
  if (token) {
    options = {
      ...options,
      headers: {
        ...options.headers,
        Authorization: `Bearer ${token}`,
      },
    };
  }
  return originalFetch(url, options);
};
```

**4. WebSocket 实时通信**

```typescript
// WebSocket Hook
function useWebSocket(url: string) {
  const [messages, setMessages] = useState<Message[]>([]);
  const wsRef = useRef<WebSocket | null>(null);
  
  useEffect(() => {
    const ws = new WebSocket(url);
    wsRef.current = ws;
    
    ws.onmessage = (event) => {
      const msg = JSON.parse(event.data);
      setMessages(prev => [...prev, msg]);
    };
    
    ws.onclose = () => {
      // 自动重连
      setTimeout(() => reconnect(), 3000);
    };
    
    return () => ws.close();
  }, [url]);
  
  const send = (data: unknown) => {
    wsRef.current?.send(JSON.stringify(data));
  };
  
  return { messages, send };
}
```
