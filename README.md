# AgentGuard - Security and Cost Control for AI Applications

> Enterprise-grade security, cost control, and guardrails for AI applications. Built to handle the complexity of autonomous agents, works with any AI API.

[![npm version](https://img.shields.io/npm/v/agentguard-sdk.svg)](https://www.npmjs.com/package/agentguard-sdk)
[![PyPI version](https://img.shields.io/pypi/v/agentguard-sdk.svg)](https://pypi.org/project/agentguard-sdk/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue.svg)](https://www.typescriptlang.org/)
[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)

## 🎉 What's New in v0.2.2

**Drop-in AI Client Wrappers with Built-in Security & Cost Control:**
- ✅ **GuardedOpenAI** - OpenAI client with automatic cost tracking and guardrails
- ✅ **GuardedAnthropic** - Anthropic client with budget enforcement
- ✅ **GuardedAzureOpenAI** - Azure OpenAI client with PII detection
- ✅ **Real-time Cost Tracking** - Track spending across 20+ AI models
- ✅ **Budget Management** - Set limits and get alerts before overspending
- ✅ **Built-in Guardrails** - PII detection, content moderation, prompt injection protection
- ✅ **100% Feature Parity** - Same experience in TypeScript and Python

**Built for the complexity of autonomous agents, works with any AI application.**

**[📖 Read the full announcement →](https://dev.to/nagasatish_chilakamarti_2/introducing-agentguard-v022-stop-ai-costs-from-spiraling-out-of-control-while-keeping-your-data-36a3)**

## 🚀 Quick Start (2 minutes)

### TypeScript/JavaScript

```bash
npm install agentguard-sdk
```

```typescript
import { GuardedOpenAI, BudgetManager } from 'agentguard-sdk';

// Create a budget
const budgetManager = new BudgetManager();
budgetManager.createBudget('my-agent', {
  amount: 10.00,  // $10 daily limit
  period: 'daily',
  action: 'block'  // Block requests when limit reached
});

// Use GuardedOpenAI instead of OpenAI
const client = new GuardedOpenAI({
  apiKey: process.env.OPENAI_API_KEY,
  agentId: 'my-agent',
  budgetManager
});

// Make requests - costs tracked automatically
const response = await client.chat.completions.create({
  model: 'gpt-4',
  messages: [{ role: 'user', content: 'Hello!' }]
});

// Check costs anytime
console.log('Total spent:', response.agentguard.cost.totalCost);
```

### Python

```bash
pip install agentguard-sdk
```

```python
from agentguard import GuardedOpenAI, BudgetManager

# Create a budget
budget_manager = BudgetManager()
budget_manager.create_budget('my-agent', {
    'amount': 10.00,  # $10 daily limit
    'period': 'daily',
    'action': 'block'
})

# Use GuardedOpenAI instead of OpenAI
client = GuardedOpenAI(
    api_key=os.environ['OPENAI_API_KEY'],
    agent_id='my-agent',
    budget_manager=budget_manager
)

# Make requests - costs tracked automatically
response = client.chat.completions.create(
    model='gpt-4',
    messages=[{'role': 'user', 'content': 'Hello!'}]
)

# Check costs anytime
print(f"Total spent: ${response.agentguard.cost.total_cost}")
```

## 🎯 Why AgentGuard?

### The Problem
- 💸 AI costs spiral out of control without visibility
- 🔓 Sensitive data leaks through AI prompts
- 🚨 No way to enforce spending limits
- 🤷 Manual cost tracking is tedious and error-prone

### The Solution
- ✅ **Automatic Cost Tracking** - Every request tracked with zero effort
- ✅ **Budget Enforcement** - Set limits and prevent overspending
- ✅ **Built-in Security** - PII detection, content moderation, prompt injection protection
- ✅ **Drop-in Replacement** - Works with existing OpenAI/Anthropic code
- ✅ **No Infrastructure** - Client-side only, no servers or databases needed

## 🚀 Overview

AgentGuard is a **client-side SDK** that provides comprehensive security controls and cost management for AI applications:

- **🛠️ Developer SDK** - Embed security controls and cost tracking with zero infrastructure
- **💰 Cost Tracking** - Automatic cost calculation for 20+ AI models
- **🛡️ Security Guardrails** - PII detection, content moderation, prompt injection protection
- **📊 Budget Management** - Set spending limits and prevent overspending

**No servers, no databases, no infrastructure required.** Just install and use!

## ✨ Key Features

### 🎯 Drop-in AI Client Wrappers
Replace your existing AI clients with zero code changes:
- **GuardedOpenAI** - Drop-in replacement for OpenAI client
- **GuardedAnthropic** - Drop-in replacement for Anthropic client  
- **GuardedAzureOpenAI** - Drop-in replacement for Azure OpenAI client

### 💰 Cost Tracking & Budget Management
- **Automatic Cost Calculation** - Track costs for 20+ AI models
- **Real-time Budget Enforcement** - Set limits and prevent overspending
- **Multi-period Budgets** - Hourly, daily, weekly, monthly, or total limits
- **Alert Thresholds** - Get notified at 50%, 75%, 90%, 100%
- **Cost Analytics** - Query costs by agent, date range, or request

### 🛡️ Built-in Guardrails
- **PII Detection** - Automatically detect and redact sensitive data (emails, SSNs, credit cards)
- **Content Moderation** - Block harmful content (hate speech, violence, harassment)
- **Prompt Injection Protection** - Detect jailbreak attempts and instruction injection
- **Custom Guardrails** - Build your own security rules

### 🚀 Developer Experience
- **No Infrastructure Required** - Everything runs client-side
- **100% Type Safe** - Full TypeScript support with IntelliSense
- **Framework Agnostic** - Works with any AI framework
- **Comprehensive Testing** - 504 tests passing (318 TypeScript, 186 Python)

## 📦 Installation

### TypeScript/JavaScript
```bash
npm install agentguard-sdk
```

### Python
```bash
pip install agentguard-sdk
```

## 📚 Examples

### Cost Tracking Example

```typescript
import { GuardedOpenAI, CostTracker } from 'agentguard-sdk';

const tracker = new CostTracker();
const client = new GuardedOpenAI({
  apiKey: process.env.OPENAI_API_KEY,
  costTracker: tracker
});

const response = await client.chat.completions.create({
  model: 'gpt-4',
  messages: [{ role: 'user', content: 'Explain quantum computing' }]
});

// Access cost information
console.log(`Estimated cost: $${response.agentguard.cost.estimatedCost}`);
console.log(`Tokens used: ${response.agentguard.cost.totalTokens}`);
```

### Budget Enforcement Example

```typescript
import { GuardedOpenAI, BudgetManager } from 'agentguard-sdk';

const budgetManager = new BudgetManager();

// Create a $50 monthly budget
budgetManager.createBudget('my-agent', {
  amount: 50.00,
  period: 'monthly',
  action: 'block',  // Block requests when limit reached
  alertThresholds: [0.5, 0.75, 0.9]  // Alert at 50%, 75%, 90%
});

const client = new GuardedOpenAI({
  apiKey: process.env.OPENAI_API_KEY,
  agentId: 'my-agent',
  budgetManager,
  onBudgetAlert: (alert) => {
    console.log(`⚠️ Budget alert: ${alert.percentage}% used`);
  }
});

// Requests automatically tracked against budget
const response = await client.chat.completions.create({
  model: 'gpt-4',
  messages: [{ role: 'user', content: 'Hello!' }]
});
```

### Guardrails Example

```typescript
import { GuardedOpenAI, PIIDetectionGuardrail } from 'agentguard-sdk';

const client = new GuardedOpenAI({
  apiKey: process.env.OPENAI_API_KEY,
  guardrails: [
    new PIIDetectionGuardrail({
      action: 'redact',  // Automatically redact PII
      patterns: ['email', 'ssn', 'credit_card']
    })
  ]
});

// PII automatically detected and redacted
const response = await client.chat.completions.create({
  model: 'gpt-4',
  messages: [{
    role: 'user',
    content: 'My email is john@example.com and SSN is 123-45-6789'
  }]
});

// Check what was detected
console.log('PII detected:', response.agentguard.guardrails.piiDetected);
```

## 📖 Documentation

- **[Getting Started Guide](docs/getting-started.md)** - Complete setup and usage
- **[FAQ](docs/FAQ.md)** - Frequently asked questions
- **[Examples](examples/)** - Working code examples
- **[Changelog](CHANGELOG.md)** - Version history and updates

## �️ Roadmap

### ✅ Phase 1: Developer SDK (v0.2.2) - COMPLETE
- [x] Drop-in AI client wrappers (OpenAI, Anthropic, Azure OpenAI)
- [x] Real-time cost tracking across 20+ models
- [x] Budget management with enforcement
- [x] Built-in guardrails (PII, content moderation, prompt injection)
- [x] TypeScript and Python SDKs with 100% feature parity
- [x] 504 comprehensive tests passing
- [x] Complete documentation and examples

### � Phase 2: Enterprise Platform (Q2-Q4 2026)
- [ ] Hosted AgentGuard service (SaaS)
- [ ] Database persistence for costs and budgets
- [ ] Advanced analytics and cost optimization
- [ ] Human-in-the-loop approval workflows
- [ ] Cryptographic audit trails
- [ ] Multi-user support with RBAC

### 🔮 Phase 3: Market Leadership (2027)
- [ ] Multi-framework support (LangChain, AutoGen, CrewAI)
- [ ] Advanced threat detection with ML
- [ ] Multi-cloud deployment
- [ ] CISO governance dashboard
- [ ] Compliance reporting (SOC 2, HIPAA, GDPR)

**[📖 View full roadmap →](docs/ROADMAP.md)**

## 🎯 Use Cases

### For Startups
- **Control AI Costs** - Prevent surprise bills from AI APIs
- **Ship Faster** - Drop-in security without infrastructure
- **Stay Compliant** - Built-in PII detection and content moderation

### For Enterprises
- **Budget Enforcement** - Set spending limits per team/agent
- **Security Guardrails** - Prevent data leaks and harmful content
- **Cost Visibility** - Track AI spending across organization

### For Developers
- **Easy Integration** - 2-minute setup, zero infrastructure
- **Type Safety** - Full TypeScript support
- **Framework Agnostic** - Works with any AI framework

## 📊 Project Stats

- **Performance**: <10ms overhead per request
- **Test Coverage**: 90%+ (TypeScript), 84%+ (Python)
- **Tests Passing**: 504 comprehensive tests
- **Models Supported**: 20+ (OpenAI, Anthropic, Azure OpenAI)
- **Languages**: TypeScript, Python (100% feature parity)

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 💬 Community & Support

- **GitHub Issues** - [Report bugs and request features](https://github.com/nagasatish007/ai-agent-security-platform/issues)
- **GitHub Discussions** - [Ask questions and share ideas](https://github.com/nagasatish007/ai-agent-security-platform/discussions)
- **Documentation** - [Getting Started Guide](docs/getting-started.md)

## � License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## � Links

- **npm**: https://www.npmjs.com/package/agentguard-sdk
- **PyPI**: https://pypi.org/project/agentguard-sdk/
- **GitHub**: https://github.com/nagasatish007/ai-agent-security-platform
- **Documentation**: [Getting Started](packages/agent-guard-sdk/README.md)

---

**⭐ Star this repo if you find it useful!**

**Made with ❤️ by developers who got tired of surprise AI bills**