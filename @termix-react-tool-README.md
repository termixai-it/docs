# @termix-it/react-tool

A configurable AI chat interface component library for React applications with advanced function calling and smart contract integration.

## Features

- 🤖 **AI Chat Interface**: Ready-to-use chat component with streaming responses
- 🔧 **Highly Configurable**: Extensive props for customization and theming
- 🛠️ **Function Calls**: Automatic AI function calling with REST API and smart contract execution
- 📚 **Knowledge Base**: Built-in knowledge base search and reference display
- 🎨 **Tailwind CSS**: Beautiful, responsive UI with customizable styling
- ⚡ **ReAct Pattern**: Support for reasoning and acting patterns in AI responses
- 🔗 **Smart Contracts**: Direct blockchain interaction through MetaMask and web3
- 📱 **Responsive**: Works seamlessly on desktop and mobile devices
- 🚀 **TypeScript**: Full TypeScript support with comprehensive type definitions

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
        welcomeMessage="Hello! How can I help you today?"
        placeholder="Type your message..."
      />
    </div>
  );
}
```

## Configuration

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
| `restExecuteHeader` | `string` | `undefined` | JSON string for custom headers in REST execution |

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

## Advanced Usage

### Custom Headers for REST API Calls

```tsx
const [customHeaders, setCustomHeaders] = useState('{"X-API-Key": "your-key"}');

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

Your backend should provide these endpoints:

- `POST /conversations` - Create new conversation
- `POST /conversations/{id}/stream` - Stream chat messages
- `POST /execute` - Execute function calls
- Knowledge base endpoints for search and retrieval

## Smart Contract Integration

The library automatically detects smart contract calls and integrates with:

- MetaMask and other web3 wallets
- Ethereum and EVM-compatible chains
- Contract read/write operations
- Transaction confirmation handling

Make sure users have a web3 wallet connected when contract execution is enabled.

## License

MIT

## Contributing

Please read our contributing guidelines and submit pull requests to help improve this library.

## Support

For issues and questions, please use the GitHub issue tracker.