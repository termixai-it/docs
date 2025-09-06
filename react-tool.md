# TermiX Frontend SDK - Easy to Use
TermiX offers a library of out-of-the-box React components that enable your dApp to support intelligent AI conversations and Web3 workflows in minutes. These components are highly customizable and can even be fully white-labeled. This means you have access to out-of-the-box natural language interaction, smart contract calls, MCP tool integration, and more.

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
// No need to import CSS - styles are now bundled with components

function App() {
  return (
    <div className="h-screen">
      <ChatInterface
        projectId="your-project-id"
        aiConfigId="your-ai-config-id"
        authorization="Bearer your-jwt-token"
        enableStreamingMode={true} // Enable real-time streaming
        placeholder="Type your message..."
      />
    </div>
  );
}
```

**Note:** 
- Styles are now automatically bundled with the components - no separate CSS import needed
- All styles are scoped with `.termix-` prefix to prevent conflicts
- The API base URL is built into the SDK and defaults to `https://dashboard.termix.ai`

## Chat Widget Component

The `ChatWidget` component provides a floating chat button with a popup dialog, perfect for customer service or help functionality. The widget includes its own header, so you typically don't need to enable `showHeader` on the ChatInterface inside it.

### Basic Widget Usage

```tsx
import { ChatWidget, ChatInterface } from '@termix-it/react-tool';

function App() {
  return (
    <div className="relative h-screen">
      {/* Your main content */}
      <div>Your application content</div>
      
      {/* Fixed positioned chat widget */}
      <div className="fixed bottom-6 right-6">
        <ChatWidget
          title="AI Assistant"
        >
          <ChatInterface
            projectId="your-project-id"
            aiConfigId="your-ai-config-id"
            authorization="Bearer your-token"
            enableStreamingMode={true}
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
| `className` | `string` | `""` | CSS classes for the widget container |
| `style` | `React.CSSProperties` | `undefined` | Inline styles for the widget container |
| `buttonClassName` | `string` | `""` | CSS classes for the chat button |
| `buttonStyle` | `React.CSSProperties` | `undefined` | Inline styles for the chat button |
| `dialogClassName` | `string` | `""` | CSS classes for the dialog |
| `dialogStyle` | `React.CSSProperties` | `undefined` | Inline styles for the dialog |
| `defaultOpen` | `boolean` | `false` | Whether dialog is open by default |
| `onOpenChange` | `(open: boolean) => void` | `undefined` | Called when dialog open state changes |
| `children` | `React.ReactNode` | - | Dialog content (usually ChatInterface) |

### Custom Button Icon

```tsx
<ChatWidget
  buttonIcon="/path/to/your/icon.png"
  title="Custom Support"
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
| `authorization` | `string` | `undefined` | Authorization header value (e.g., 'Bearer token') |
| `apiHeaders` | `Record<string, string>` | `{}` | Additional headers for API requests |
| `restExecuteHeader` | `Record<string, string>` | `undefined` | Custom headers object for REST execution |

### UI Configuration

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `placeholder` | `string` | `"Type your message..."` | Input placeholder text |
| `sendButtonText` | `string` | `""` | Send button text (empty string shows default icon) |
| `modelName` | `string` | `"AI Model"` | Fallback model name if API config fetch fails |
| `personalityName` | `string` | `undefined` | Optional override for personality name (overrides API config value) |

### Feature Toggles

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `enableStreamingMode` | `boolean` | `false` | Enable real-time streaming responses via SSE |
| `showHeader` | `boolean` | `false` | Show/hide the chat header with title and model info |
| `showUsageInfo` | `boolean` | `false` | Show token usage and cost information |
| `showTimestamp` | `boolean` | `false` | Show message timestamps |
| `maxKnowledgeResults` | `number` | `3` | Maximum knowledge base results to show |

**Note:** The following features are now always enabled and cannot be disabled:
- Knowledge base integration
- Function calls (REST API and smart contracts)
- ReAct pattern (reasoning and acting)
- Knowledge references display

### Styling Props

| Prop | Type | Description |
|------|------|-------------|
| `className` | `string` | Additional CSS classes for the main container |
| `style` | `React.CSSProperties` | Inline styles for the main container |
| `messagesClassName` | `string` | CSS classes for the messages area |
| `messagesStyle` | `React.CSSProperties` | Inline styles for the messages area |
| `inputClassName` | `string` | CSS classes for the input field |
| `inputStyle` | `React.CSSProperties` | Inline styles for the input field |

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
// Pass custom headers as an object
const customHeaders = { "X-API-Key": "your-key", "X-Custom": "value" };

<ChatInterface
  projectId="your-project-id"
  aiConfigId="your-ai-config-id"
  authorization="Bearer your-token"
  restExecuteHeader={customHeaders} // Pass object directly, not as string
  // ... other props
/>
```

### Function Call Handling

```tsx
<ChatInterface
  // ... required props
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
  const customHeaders = { "X-API-Key": "your-key", "X-Custom": "value" };

  return (
    <ChatInterface
      projectId="689b0b0a67504c373d86bed6"
      aiConfigId="689b0ce8ed28bfae5038fe82"
      authorization={authorization}
      restExecuteHeader={customHeaders}
      
      // Features configuration
      enableStreamingMode={true} // Enable real-time streaming
      showHeader={true} // Show chat header with model info
      showUsageInfo={true} // Optional: show token usage
      showTimestamp={true} // Optional: show timestamps
      maxKnowledgeResults={5} // Max knowledge base results to show
      
      // Customization
      placeholder="Ask me anything..."
      sendButtonText="" // Empty string shows icon
      modelName="GPT-4" // Fallback if API config fetch fails
      personalityName="Advanced Assistant" // Optional: override API config personality name
      
      // Callbacks
      onMessageSent={(message) => console.log('Sent:', message)}
      onResponseReceived={(message) => console.log('Received:', message)}
      onFunctionExecuted={(call, result) => console.log('Executed:', call, result)}
      onError={(error) => console.error('Error:', error)}
    />
  );
}
```

## Important Changes in Latest Version

### Automatic Feature Enablement
The following features are now **always enabled** and cannot be disabled (they are hardcoded as true in the component):
- **Knowledge Base Integration**: Automatically searches and references knowledge base
- **Function Calls**: AI can execute REST APIs and smart contracts
- **ReAct Pattern**: Reasoning and acting pattern for complex tasks
- **Knowledge References**: Always displays knowledge base references when available

These previously configurable props have been removed:
- `enableKnowledgeBase` (always true)
- `enableFunctionCalls` (always true)
- `enableReActPattern` (always true)
- `showKnowledgeReferences` (always true)

### Welcome Message and Personality from API
The component now automatically fetches configuration from the AI config API:
1. **Welcome Message**: Uses greeting from API config or generates default
2. **Personality Name**: Uses name from API config, can be overridden with `personalityName` prop
3. **Re-fetching**: Automatically re-fetches when `projectId` or `aiConfigId` changes

Default fallback: `"Hello! I'm [personality name]. How can I help you today?"`

### Default Values
- `sendButtonText`: Now defaults to `""` (empty string shows icon instead of text)
- `showUsageInfo`: Defaults to `false`
- `showTimestamp`: Defaults to `false`
- `showHeader`: Defaults to `false`
- `enableStreamingMode`: Defaults to `false`

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

The styles are now **automatically bundled** with the components - no separate CSS import needed. All styles are scoped with `.termix-` prefix to prevent conflicts with your application's styles.

### Using Inline Styles

Both `ChatInterface` and `ChatWidget` support inline styles via the `style` prop:

```tsx
// ChatInterface with custom styles
<ChatInterface
  projectId="your-project-id"
  aiConfigId="your-ai-config-id"
  style={{ 
    height: '600px', 
    borderRadius: '12px',
    boxShadow: '0 4px 6px rgba(0,0,0,0.1)'
  }}
  messagesStyle={{ 
    backgroundColor: '#f9f9f9' 
  }}
  inputStyle={{ 
    fontSize: '16px',
    padding: '12px 16px'
  }}
/>

// ChatWidget with custom button and dialog styles
<ChatWidget
  style={{ position: 'fixed', bottom: '20px', right: '20px' }}
  buttonStyle={{ 
    width: '60px', 
    height: '60px',
    backgroundColor: '#6366f1'
  }}
  dialogStyle={{ 
    width: '400px',
    height: '500px',
    borderRadius: '16px'
  }}
>
  <ChatInterface {...props} />
</ChatWidget>
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

### Default API Configuration

The SDK now automatically connects to the Termix API:
- **Production**: `https://dashboard.termix.ai`
- **Local Development**: `http://127.0.0.1:3001` (when using `npm run dev:local`)

```tsx
<ChatInterface
  projectId="your-project-id"
  aiConfigId="your-ai-config-id"
  authorization="Bearer your-token"
  enableStreamingMode={true}
  // ... other props
/>
```

### Development

For local development with a local backend server:

1. **Install the SDK in your project:**
   ```bash
   npm install @termix-it/react-tool
   ```

2. **For local backend development:**
   
   If you need to connect to a local backend server running at `http://127.0.0.1:3001`, you have two options:
   
   **Option 1: Build the SDK locally with local configuration**
   ```bash
   # In the react-tool directory
   npm run dev:local
   
   # Then link it to your project
   npm link
   
   # In your project directory
   npm link @termix-it/react-tool
   ```
   
   **Option 2: Use environment variable (if your build system supports it)**
   ```bash
   # Set the environment variable before building
   REACT_APP_API_LOCAL=true npm run build
   ```

The SDK will automatically connect to these Termix API endpoints:

### Chat Endpoints
- `POST /api/v1/ai/projects/{projectId}/chat` - Regular chat messages
- `POST /api/v1/ai/projects/{projectId}/chat/stream` - Streaming chat messages (SSE)
- `GET /api/v1/ai/projects/{projectId}/configs/{configId}` - Get AI config (including greeting message)

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

You must manually import the styles. If you experience issues:

1. **Check for CSS conflicts**: The library's styles are scoped to `.termix-container` to avoid conflicts, but ensure your global styles don't override them.

2. **Tailwind CSS conflicts**: If your project uses Tailwind CSS, the scoped styles should prevent conflicts. The components also use inline styles for critical styling.

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