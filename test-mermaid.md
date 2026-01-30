# Mermaid 图表测试

## 测试 1: 核心流程图

```mermaid
graph TB
    Start([User Starts System]) --> Init[Initialize Client]
    Init --> Auth{Authenticated?}
    Auth -->|No| Login[Login Flow]
    Auth -->|Yes| LoadSession[Load Session]
    Login --> SaveSession[Save Session]
    LoadSession --> Connect[Connect to Server]
    SaveSession --> Connect

    Connect --> Dashboard[Launch Dashboard]
    Dashboard --> UserAction{User Action}

    UserAction -->|Action A| ActionA[Execute Action A]
    UserAction -->|Action B| ActionB[Execute Action B]

    ActionA --> Process[Processing Flow]
    ActionB --> Process

    Process --> Result[Save Result]
    Result --> Notify[Notify User]

    Notify --> Dashboard

    style Start fill:#e1f5e1
    style Dashboard fill:#e3f2fd
    style Process fill:#fff3e0
    style Notify fill:#fce4ec
```

## 测试 2: 数据流程图

```mermaid
sequenceDiagram
    participant U as User
    participant F as Frontend
    participant B as Backend API
    participant D as Database
    participant E as External Service

    U->>F: 1. Initiate Request
    F->>B: 2. API Call
    B->>D: 3. Query Data
    D-->>B: 4. Return Data
    B-->>F: 5. Return JSON
    F-->>U: 6. Display Result

    U->>F: 7. Trigger Action
    F->>B: 8. POST Request
    B->>D: 9. Create Task
    D-->>B: 10. Return Task ID
    B-->>F: 11. Return { taskId: 123 }
    F-->>U: 12. Show Progress

    B->>E: 13. Call External Service
    E-->>B: 14. Return Result
    B->>D: 15. Save Result
    B->>F: 16. Push Notification
    F-->>U: 17. Show Completion
```

## 测试 3: 技术架构图（修复后）

```mermaid
graph LR
    subgraph FrontendLayer[Frontend Layer]
        Web[React + Vite]
        UI[UI Component Library]
        State[State Management]
    end

    subgraph BackendLayer[Backend Layer]
        API[API Server<br/>Framework Name]
        Service1[Service 1<br/>Function Description]
        Service2[Service 2<br/>Function Description]
        Scheduler[Scheduled Tasks<br/>Tool Name]
    end

    subgraph DataLayer[Data Layer]
        DB[(Database<br/>Type)]
        ORM[ORM Tool]
        Cache[(Cache<br/>Type)]
    end

    subgraph ExternalServices[External Services]
        External1[External Service 1]
        External2[External Service 2]
    end

    Web --> API
    UI --> Web
    State --> Web

    API --> Service1
    API --> Service2
    API --> Scheduler
    API --> ORM

    Service1 --> External1
    Service2 --> External2
    ORM --> DB
    API --> Cache

    style Web fill:#61dafb
    style API fill:#ff6b6b
    style DB fill:#4caf50
    style External1 fill:#0088cc
    style External2 fill:#ff9800
```

## 修复说明

**问题原因**：GitHub 的 Mermaid 渲染器对 `subgraph "Name"` 语法支持不完善，会导致 "Could not find a suitable point for the given distance" 错误。

**解决方案**：使用 `subgraph ID[Name]` 语法替代 `subgraph "Name"`，这样可以：
1. 避免引号导致的解析问题
2. 提供明确的节点 ID
3. 提高 GitHub 渲染兼容性

**修改内容**：
- `subgraph "Frontend Layer"` → `subgraph FrontendLayer[Frontend Layer]`
- `subgraph "Backend Layer"` → `subgraph BackendLayer[Backend Layer]`
- `subgraph "Data Layer"` → `subgraph DataLayer[Data Layer]`
- `subgraph "External Services"` → `subgraph ExternalServices[External Services]`
