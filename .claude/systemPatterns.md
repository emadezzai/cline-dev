# System Architecture

## High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    VSCode Extension Host                     │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │Extension.ts │──│WebviewProvider│──│   Controller        │  │
│  │ (entry point)│  │(manages UI)  │  │  (state manager)    │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
│                                                 │           │
│  ┌──────────────────────────────────────────────┼────────┐  │
│  │                    Task                       │        │  │
│  │  (executes AI requests and tool operations)  │        │  │
│  └──────────────────────────────────────────────┼────────┘  │
│                                    │                        │
│  ┌─────────────────────────────────┼────────────────────┐  │
│  │           McpHub                │                    │  │
│  │  (MCP server connections)       │  Api Providers     │  │
│  └─────────────────────────────────┴────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      Webview UI (React)                      │
│  ┌───────────────────────────────────────────────────────┐  │
│  │              ExtensionStateContext                     │  │
│  │  (React context for managing UI state)                │  │
│  └───────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

## Component Relationships

### Core Extension (src/)
- **extension.ts**: نقطة الدخول الرئيسية
- **WebviewProvider**: يدير دورة حياة الـ webview والتواصل
- **Controller**: يدير حالة الامتداد والموارد
- **Task**: ينفذ طلبات API وعمليات الأدوات
- **McpHub**: يدير اتصالات خوادم MCP

### API Providers (src/api/providers/)
- Anthropic, OpenRouter, AWS Bedrock, Gemini, Ollama, LM Studio, إلخ

### Webview (webview-ui/)
- React app مع TypeScript
- ExtensionStateContext للتواصل مع الـ extension
- مكونات React للواجهة

## Key Design Patterns

### 1. gRPC-like Communication
التواصل بين الـ extension والـ webview يتم عبر VSCode message passing مع بروتوكول مشابه لـ gRPC. التعريفات في `proto/` directory.

### 2. State Management
- **Controller**: مصدر الحقيقة الرئيسي لحالة الامتداد
- **ExtensionStateContext**: يدير حالة الـ webview في React
- **Global State**: مخزن عبر جميع نافذات VSCode
- **Workspace State**: خاص للمشروع الحالي
- **Secrets**: تخزين آمن للمفاتيح

### 3. Task Execution Loop
```
Task Loop:
1. Make API request and stream response
2. Parse and present content blocks
3. Wait for tool execution approval
4. Execute tool and return result
5. Continue loop with tool result
```

### 4. Context Management
نظام لإدارة تاريخ المحادثة وتقصيره عند الحاجة لتجنب تجاوز context window.

### 5. Checkpoint System
لقطات Git-based للعمل للمقارنة والاستعادة.
