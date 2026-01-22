# Technical Context

## Technologies Used

### Core Extension
- **Language**: TypeScript 5.4+
- **VSCode API**: ^1.84.0
- **Build**: esbuild
- **Testing**: Mocha + VSCode Test

### Frontend (Webview)
- **Framework**: React
- **Language**: TypeScript
- **Build**: Vite
- **Styling**: Tailwind CSS 4

### API & Communication
- **Protocol Buffers**: للتعريفات ونظام الاتصال
- **nice-grpc**: gRPC client
- **axios**: HTTP client مع دعم proxy

### AI Providers
- **Anthropic SDK**: ^0.37.0
- **OpenAI**: ^6.9.0
- **Google GenAI/VertexAI**: للـ Gemini
- **AWS Bedrock**: عبر @aws-sdk
- **Ollama**: عبر ollama library
- **LM Studio**: دعم محلي
- **OpenRouter**: دعم متعدد النماذج

### MCP (Model Context Protocol)
- **@modelcontextprotocol/sdk**: ^1.25.1

### Browser Automation
- **Puppeteer Core**: ^23.4.0

### Storage
- **better-sqlite3**: قاعدة بيانات محلية
- **VSCode Global/Workspace State**: للتخزين المستمر

### Terminal Integration
- **shell-quote**: لتحليل الأوامر
- VSCode Terminal Shell Integration API

### Other Libraries
- **diff**: لحساب الفروقات
- **turndown**: HTML to Markdown
- **zod**: للتحقق من الـ schema
- **uuid**: لمعرفات فريدة
- **posthog-node**: تحليلات

## Development Setup

### Installation
```bash
npm install
cd webview-ui && npm install
```

### Development
```bash
npm run dev              # يشمل protos + watch
npm run dev:webview      # تطوير الـ webview فقط
npm run protos           # بناء ملفات الـ proto
```

### Building
```bash
npm run compile          # بناء الامتداد
npm run build:webview    # بناء الـ webview
npm run package          # تجميع للتوزيع
```

### Testing
```bash
npm run test:unit        # اختبارات الوحدة
npm run test:integration # اختبارات التكامل
npm run test:e2e         # اختبارات end-to-end
```

### Code Quality
```bash
npm run check-types      # فحص الأنواع
npm run lint             # فحص الكود
npm run format           # تنسيق الكود
```

## Project Structure

```
/
├── proto/                    # Protobuf definitions
│   ├── cline/                # Cline-specific messages
│   └── host/                 # Host communication
├── src/
│   ├── core/
│   │   ├── controller/       # Main controller
│   │   ├── webview/          # Webview provider
│   │   ├── task/             # Task execution
│   │   ├── prompts/          # System prompts
│   │   └── tools/            # Tool implementations
│   ├── api/
│   │   └── providers/        # API provider implementations
│   ├── services/
│   │   └── mcp/              # MCP hub and servers
│   ├── shared/
│   │   ├── proto/            # Generated proto types
│   │   ├── storage/          # State management
│   │   └── utils/            # Utilities
│   └── hosts/                # gRPC host implementations
├── webview-ui/
│   └── src/
│       ├── components/       # React components
│       ├── context/          # React contexts
│       ├── services/         # gRPC clients
│       └── hooks/            # Custom hooks
└── cli/                      # CLI application (Go)
```

## Important Configuration Files

- **buf.yaml**: protobuf configuration
- **tsconfig.json**: TypeScript config
- **biome.jsonc**: Biome linter/formatter config
- **knip.json**: Unused dependency checker
