# @termix-it/react-tool

TermiX offers a library of out-of-the-box React components that enable your dApp to support intelligent AI conversations and Web3 workflows in minutes. These components are highly customizable and can even be fully white-labeled. This means you have access to out-of-the-box natural language interaction, smart contract calls, MCP tool integration, and more..

## Features

- 🤖 **AI Chat Interface**: Ready-to-use chat component with real-time streaming responses
- 🔧 **Highly Configurable**: Extensive props for customization and theming
- 🛠️ **Function Calls**: Automatic AI function calling with REST API and smart contract execution
- 📚 **Knowledge Base**: Built-in knowledge base search and reference display
- 🎨 **Tailwind CSS**: Beautiful, responsive UI with customizable styling
- ⚡ **ReAct Pattern**: Support for reasoning and acting patterns in AI responses
- 🔗 **Smart Contracts**: Direct blockchain interaction through MetaMask and web3
- 📱 **Responsive**: Works seamlessly on desktop and mobile devices
- 🚀 **TypeScript**: Full TypeScript support with comprehensive type definitions
- 🌊 **Real-time Streaming**: Server-Sent Events (SSE) support for live chat responses

## Installation

```bash
npm install @termix-it/react-tool
# or
yarn add @termix-it/react-tool
# or
pnpm add @termix-it/react-tool
```

## Dependencies

This library requires the following peer dependencies:

```json
{
  "react": ">=16.9.0",
  "react-dom": ">=16.9.0"
}
```

## Quick Start

### Basic Usage

```tsx
import { ChatInterface } from '@termix-it/react-tool';
import '@termix-it/react-tool/dist/styles.css'; // Import required styles

function App() {
  return (
    <div className="h-screen">
      <ChatInterface
        projectId="your-project-id"
        aiConfigId="your-ai-config-id"
        apiBaseUrl="/api/proxy"
        authorization="Bearer your-jwt-token"
        enableStreamingMode={true} // Enable real-time streaming
        welcomeMessage="Hello! How can I help you today?"
        placeholder="Type your message..."
      />
    </div>
  );
}
```

## Chat Widget Component

The `ChatWidget` component provides a floating chat button with a popup dialog, perfect for customer service or help functionality. The widget includes its own header, so you typically don't need to enable `showHeader` on the ChatInterface inside it.

### Basic Widget Usage

```tsx
import { ChatWidget, ChatInterface } from '@termix-it/react-tool';
import '@termix-it/react-tool/dist/styles.css';

function App() {
  return (
    <div className="relative h-screen">
      {/* Your main content */}
      <div>Your application content</div>
      
      {/* Fixed positioned chat widget */}
      <div className="fixed bottom-6 right-6">
        <ChatWidget
          title="AI Assistant"
          subtitle="智能助手为您服务"
        >
          <ChatInterface
            projectId="your-project-id"
            aiConfigId="your-ai-config-id"
            apiBaseUrl="/api/proxy"
            authorization="Bearer your-token"
            enableStreamingMode={true}
            welcomeMessage="Hello! How can I help you?"
            className="h-full"
          />
        </ChatWidget>
      </div>
    </div>
  );
}
```

### ChatWidget Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `buttonIcon` | `string` | `undefined` | Custom button icon URL |
| `title` | `string` | `"AI Assistant"` | Dialog header title |
| `subtitle` | `string` | `"智能助手为您服务"` | Dialog header subtitle |
| `className` | `string` | `""` | CSS classes for the widget container |
| `buttonClassName` | `string` | `""` | CSS classes for the chat button |
| `dialogClassName` | `string` | `""` | CSS classes for the dialog |
| `defaultOpen` | `boolean` | `false` | Whether dialog is open by default |
| `onOpenChange` | `(open: boolean) => void` | `undefined` | Called when dialog open state changes |
| `children` | `React.ReactNode` | - | Dialog content (usually ChatInterface) |

### Custom Button Icon

```tsx
<ChatWidget
  buttonIcon="/path/to/your/icon.png"
  title="Custom Support"
  subtitle="We're here to help!"
>
  <ChatInterface {...chatProps} />
</ChatWidget>
```

### Controlled State

```tsx
function ControlledWidget() {
  const [isOpen, setIsOpen] = useState(false);
  
  return (
    <ChatWidget
      defaultOpen={isOpen}
      onOpenChange={setIsOpen}
      title="Support Chat"
    >
      <ChatInterface {...chatProps} />
    </ChatWidget>
  );
}
```

## Configuration

### Chat Header

The ChatInterface component includes an optional header that displays the AI model name and personality. Control it with the `showHeader` prop:

```tsx
<ChatInterface
  showHeader={true}  // Default: false
  modelName="GPT-4"
  personalityName="AI Assistant"
  showUsageInfo={true}  // Shows total cost in header when available
  // ... other props
/>
```

The header features:
- Blue gradient background with white text
- Model and personality name display
- Optional usage cost display (when `showUsageInfo` is true)
- Automatically hidden by default for cleaner integration

### Required Props

| Prop | Type | Description |
|------|------|-------------|
| `projectId` | `string` | Your Termix project identifier |
| `aiConfigId` | `string` | AI configuration identifier |

### Authentication & API

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `apiBaseUrl` | `string` | `''` | Base URL for API requests |
| `authorization` | `string` | `undefined` | Authorization header value (e.g., 'Bearer token') |
| `apiHeaders` | `Record<string, string>` | `{}` | Additional headers for API requests |
| `restExecuteHeader` | `Record<string, string>` | `undefined` | Custom headers object for REST execution |

### UI Configuration

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `welcomeMessage` | `string` | `"Hello! I'm your AI assistant..."` | Initial greeting message |
| `placeholder` | `string` | `"Type your message..."` | Input placeholder text |
| `sendButtonText` | `string` | `"Send"` | Send button text |
| `modelName` | `string` | `undefined` | Display name for the AI model |
| `personalityName` | `string` | `undefined` | Display name for the AI personality |

### Feature Toggles

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `enableKnowledgeBase` | `boolean` | `true` | Enable knowledge base search integration |
| `enableFunctionCalls` | `boolean` | `true` | Enable AI function calling and execution |
| `enableReActPattern` | `boolean` | `true` | Enable ReAct reasoning pattern |
| `enableStreamingMode` | `boolean` | `false` | Enable real-time streaming responses via SSE |
| `showHeader` | `boolean` | `false` | Show/hide the chat header with title and model info |
| `showUsageInfo` | `boolean` | `true` | Show token usage and cost information |
| `showTimestamp` | `boolean` | `true` | Show message timestamps |
| `showKnowledgeReferences` | `boolean` | `true` | Show knowledge base references |
| `maxKnowledgeResults` | `number` | `3` | Maximum knowledge base results to show |

### Styling Props

| Prop | Type | Description |
|------|------|-------------|
| `className` | `string` | Additional CSS classes for the main container |
| `messagesClassName` | `string` | CSS classes for the messages area |
| `inputClassName` | `string` | CSS classes for the input field |

### Event Callbacks

| Prop | Type | Description |
|------|------|-------------|
| `onMessageSent` | `(message: Message) => void` | Called when user sends a message |
| `onResponseReceived` | `(message: Message) => void` | Called when AI responds |
| `onFunctionExecuted` | `(functionCall: FunctionCall, result: ExecutionResult) => void` | Called when a function is executed |
| `onError` | `(error: any) => void` | Called when an error occurs |

## Streaming Mode

The ChatInterface supports real-time streaming responses using Server-Sent Events (SSE). When enabled, messages appear character by character as they are received from the server.

### Basic Streaming Setup

```tsx
<ChatInterface
  projectId="your-project-id"
  aiConfigId="your-ai-config-id"
  apiBaseUrl="/api/proxy"
  authorization="Bearer your-token"
  enableStreamingMode={true} // Enable streaming
  // ... other props
/>
```

### Streaming Endpoint Requirements

When `enableStreamingMode={true}`, the component will use:
- **Endpoint**: `POST /api/v1/ai/projects/{projectId}/chat/stream`
- **Content-Type**: `application/json`
- **Accept**: `text/event-stream`

The endpoint should return SSE events in this format:

```
data: {"type":"content","data":"Hello"}
data: {"type":"content","data":" there!"}
data: {"type":"done","sessionId":"session-id-here"}
```

### Stream Event Types

- `{"type":"content","data":"..."}` - Partial message content
- `{"type":"done","sessionId":"..."}` - Stream completion with session ID

### Streaming vs Regular Mode

| Feature | Regular Mode | Streaming Mode |
|---------|-------------|----------------|
| Endpoint | `/chat` | `/chat/stream` |
| Response | Complete message | Character-by-character |
| Usage Info | Available | Limited (cost not tracked) |
| Visual Feedback | Loading spinner | Real-time typing |
| Network | Single request | SSE connection |

## Advanced Usage

### Custom Headers for REST API Calls

```tsx
const customHeaders = { "X-API-Key": "your-key", "X-Custom": "value" };

<ChatInterface
  projectId="your-project-id"
  aiConfigId="your-ai-config-id"
  authorization="Bearer your-token"
  restExecuteHeader={customHeaders}
  // ... other props
/>
```

### Function Call Handling

```tsx
<ChatInterface
  // ... required props
  enableFunctionCalls={true}
  onFunctionExecuted={(functionCall, result) => {
    console.log('Function executed:', functionCall.name);
    
    // Handle different function types
    if (functionCall.metadata?.type === 'contract' && result.success) {
      if (result.data?.transactionHash) {
        console.log('Transaction hash:', result.data.transactionHash);
        // Show transaction confirmation UI
      }
    }
    
    if (functionCall.metadata?.type === 'api') {
      console.log('API call result:', result.data);
      // Handle API response
    }
  }}
  onError={(error) => {
    console.error('Chat error:', error);
    // Handle errors appropriately
  }}
/>
```

### Complete Feature Example

```tsx
export default function AdvancedChat() {
  const [authorization, setAuthorization] = useState('Bearer your-token');
  const [customHeaders, setCustomHeaders] = useState('{}');

  return (
    <ChatInterface
      projectId="689b0b0a67504c373d86bed6"
      aiConfigId="689b0ce8ed28bfae5038fe82"
      apiBaseUrl="/api/proxy"
      authorization={authorization}
      restExecuteHeader={customHeaders}
      
      // Enable all features
      enableKnowledgeBase={true}
      enableFunctionCalls={true}
      enableReActPattern={true}
      enableStreamingMode={true} // Enable real-time streaming
      showHeader={true} // Show chat header with model info
      showUsageInfo={true}
      showTimestamp={true}
      showKnowledgeReferences={true}
      
      // Customization
      welcomeMessage="Welcome! I can help with API calls, smart contracts, and more."
      placeholder="Ask me anything..."
      modelName="GPT-4"
      personalityName="Advanced Assistant"
      
      // Callbacks
      onMessageSent={(message) => console.log('Sent:', message)}
      onResponseReceived={(message) => console.log('Received:', message)}
      onFunctionExecuted={(call, result) => console.log('Executed:', call, result)}
      onError={(error) => console.error('Error:', error)}
    />
  );
}
```

## Function Calling

The ChatInterface automatically handles different types of function calls:

### API Calls
- REST API endpoints are automatically executed
- Custom headers can be provided via `restExecuteHeader`
- Supports GET, POST, PUT, DELETE methods
- Returns formatted response data

### Smart Contract Calls
- Automatically detects contract function calls
- Integrates with MetaMask and web3 providers
- Supports both read and write operations
- Shows transaction hashes and confirmations

### Built-in Functions
- Knowledge base search
- Data analysis and processing
- File operations (when configured)

## Styling

This library uses Tailwind CSS for styling. Import the required styles:

```tsx
import '@termix-it/react-tool/dist/styles.css';
```

### Custom Theming

You can override the default colors using CSS custom properties:

```css
:root {
  --primary: 220 100% 50%;
  --primary-foreground: 0 0% 100%;
  --secondary: 210 40% 96%;
  --secondary-foreground: 222.2 84% 4.9%;
  --accent: 210 40% 96%;
  --accent-foreground: 222.2 84% 4.9%;
  --destructive: 0 84.2% 60.2%;
  --destructive-foreground: 210 40% 98%;
  --border: 214.3 31.8% 91.4%;
  --input: 214.3 31.8% 91.4%;
  --ring: 222.2 84% 4.9%;
}
```

## TypeScript Support

Full TypeScript support with exported types:

```tsx
import type { 
  Message, 
  ToolCall,
  KnowledgeContext,
  FunctionCall,
  ExecutionResult,
  ChatInterfaceProps,
  APIConfig
} from '@termix-it/react-tool';

// Example usage
const handleFunctionCall = (
  functionCall: FunctionCall, 
  result: ExecutionResult
) => {
  if (result.success && result.type === 'contract') {
    // Handle successful contract execution
  }
};
```

### Type Definitions

```tsx
interface Message {
  id: string;
  role: 'user' | 'assistant' | 'system';
  content: string;
  timestamp: Date;
  usage?: {
    promptTokens: number;
    completionTokens: number;
    totalTokens: number;
    cost: number;
  };
  knowledgeContext?: KnowledgeContext[];
  toolCalls?: ToolCall[];
}

interface FunctionCall {
  name: string;
  parameters: Record<string, any>;
  metadata?: {
    type?: 'api' | 'contract' | 'unknown';
    description?: string;
    method?: string;
    path?: string;
    contractName?: string;
    contractAddress?: string;
    chainName?: string;
  };
}

interface ExecutionResult {
  success: boolean;
  type: 'api' | 'contract' | 'error';
  data?: any;
  error?: string;
  metadata?: Record<string, any>;
}
```

## Exported Components and Utilities

```tsx
// Main components
export { ChatInterface } from './components/ChatInterface';
export { ChatWidget } from './components/ChatWidget';
export { FunctionCallDisplay } from './components/FunctionCallDisplay';

// Services
export { APIService } from './services/api';
export { FunctionCallExecutor } from './services/functionCallExecutor';
export { ToolCallProcessor } from './services/toolCallProcessor';

// Utilities
export { cn, extractFunctionCalls } from './lib/utils';

// Hooks
export { useToast } from './hooks/useToast';
```

## API Integration

### Direct API Usage

For direct integration with Termix API:

```tsx
<ChatInterface
  projectId="your-project-id"
  aiConfigId="your-ai-config-id"
  apiBaseUrl="https://api.termix.it"
  authorization="Bearer your-token"
  enableStreamingMode={true}
  // ... other props
/>
```

### Proxy Configuration

For development or when using a proxy server:

```tsx
<ChatInterface
  projectId="your-project-id"
  aiConfigId="your-ai-config-id"
  apiBaseUrl="/api/proxy"
  authorization="Bearer your-token"
  enableStreamingMode={true}
  // ... other props
/>
```

Your proxy should forward requests to these Termix API endpoints:

### Chat Endpoints
- `POST /api/v1/ai/projects/{projectId}/chat` - Regular chat messages
- `POST /api/v1/ai/projects/{projectId}/chat/stream` - Streaming chat messages (SSE)

### Function Execution
- REST API endpoints for function calls (auto-detected)
- Smart contract execution via web3 providers

### Knowledge Base
- `GET /api/v1/projects/{projectId}/knowledge-base/search` - Search knowledge base
- `GET /api/v1/knowledge/{projectId}` - Get all knowledge

### MCP Tools
- `GET /api/v1/mcp-tools/{projectId}/parsed-endpoints` - Get parsed API endpoints
- `GET /api/v1/mcp-tools/{projectId}/parsed-contracts` - Get parsed smart contracts

### Example Proxy Implementation

For Next.js applications, you can create API routes to proxy requests:

```typescript
// pages/api/proxy/v1/ai/projects/[projectId]/chat/stream/route.ts
import { NextRequest } from 'next/server';

export async function POST(request: NextRequest) {
  const { projectId } = await request.params;
  const body = await request.json();
  const authorization = request.headers.get('authorization');

  const response = await fetch(`https://api.termix.it/api/v1/ai/projects/${projectId}/chat/stream`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': authorization!,
      'Accept': 'text/event-stream',
    },
    body: JSON.stringify(body),
  });

  return new Response(response.body, {
    headers: {
      'Content-Type': 'text/event-stream',
      'Cache-Control': 'no-cache',
      'Connection': 'keep-alive',
    },
  });
}
```

## Smart Contract Integration

The library automatically detects smart contract calls and integrates with:

- MetaMask and other web3 wallets
- Ethereum and EVM-compatible chains
- Contract read/write operations
- Transaction confirmation handling

Make sure users have a web3 wallet connected when contract execution is enabled.

## Troubleshooting

### Styles Not Loading Correctly

If you experience issues with styles (e.g., white text on white background), ensure:

1. **Import the CSS file**:
   ```tsx
   import '@termix-it/react-tool/dist/styles.css';
   ```

2. **Check Tailwind CSS conflicts**: If your project uses Tailwind CSS, there might be conflicts. The components use inline styles for critical styling to avoid this issue.

3. **Header visibility**: The chat header uses inline styles to ensure proper display:
   - Blue gradient background: `linear-gradient(to right, #3b82f6, #2563eb)`
   - White text color is explicitly set

### Input Alignment Issues

The input area automatically aligns the text input and send button vertically. If you experience alignment issues, check that parent containers don't override the flex layout.

## License

MIT

## Contributing

Please read our contributing guidelines and submit pull requests to help improve this library.

## Support

For issues and questions, please use the GitHub issue tracker.