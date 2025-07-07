# UAEngine Repository Integration Guide

## Quick Start by Use Case

### 1. Open Source Project Integration

```bash
# Clone only the open source components
git clone https://github.com/UAEngine/uaengine-core.git
git clone https://github.com/UAEngine/uaengine-memory.git
git clone https://github.com/UAEngine/uaengine-sdk.git

# Install
pip install uaengine-core uaengine-memory

# Use in your project
from uaengine import UAEngineIntegration

engine = UAEngineIntegration()
await engine.initialize()

# Must comply with AGPL for memory component
# Your project must be open source if using memory component
```

### 2. Commercial Integration

```bash
# Install with commercial license
pip install uaengine-enterprise

# Configure license
export UAENGINE_LICENSE_KEY="your-license-key"

# Use all components
from uaengine_enterprise import UAEngineEnterprise

engine = UAEngineEnterprise(license_key=os.getenv("UAENGINE_LICENSE_KEY"))
await engine.initialize()

# No open source requirements with commercial license
```

### 3. Plugin Development

```bash
# Use the plugin template
git clone https://github.com/UAEngine/uaengine-plugin-template.git my-plugin

# Develop your plugin
cd my-plugin
# Edit plugin.json and main.py

# Choose your license model
# - Open source: Share freely
# - Proprietary: Sell through UAEngine marketplace
```

## Component Interaction Map

```
┌─────────────────────┐     ┌─────────────────────┐
│   uaengine-core     │────▶│  Your Application   │
│   (Apache 2.0)      │     │                     │
└──────────┬──────────┘     └──────────┬──────────┘
           │                           │
           ▼                           ▼
┌─────────────────────┐     ┌─────────────────────┐
│  uaengine-memory    │     │   Custom Plugins    │
│    (AGPL 3.0)       │     │  (Your License)     │
└──────────┬──────────┘     └─────────────────────┘
           │
           ▼
┌─────────────────────┐
│ uaengine-algorithms │
│  (Proprietary)      │
│ (License Key Req.)  │
└─────────────────────┘
```

## License Compliance Matrix

| Component | Open Source Use | Commercial Use | Attribution | Share Modifications |
|-----------|-----------------|----------------|-------------|-------------------|
| Core | ✓ Free | ✓ Free | Required | Not Required |
| Memory | ✓ Free | License Required | Required | Required (AGPL) |
| Algorithms | Research Only | License Required | Required | Not Allowed |
| Enterprise | Not Available | License Required | Optional | Not Required |

## Integration Examples

### Basic Open Source Usage

```python
import asyncio
from uaengine import UAEngineCore
from uaengine.memory import FiveLayerMemory

async def main():
    # Initialize core engine
    engine = UAEngineCore()
    
    # Add memory system (AGPL - must share modifications)
    memory = FiveLayerMemory()
    engine.register_component(memory)
    
    # Optimize something
    result = await engine.optimize({
        'type': 'database',
        'query': 'SELECT * FROM users'
    })
    
    print(f"Performance improvement: {result.improvement}%")
    print("Powered by UAEngine")  # Required attribution

asyncio.run(main())
```

### Commercial Usage with All Features

```python
import asyncio
from uaengine_enterprise import UAEngineEnterprise

async def main():
    # Initialize with license key
    engine = UAEngineEnterprise(
        license_key="YOUR-LICENSE-KEY",
        enable_telemetry=True
    )
    
    # All features available
    await engine.enable_quantum_acceleration()
    await engine.enable_neural_optimization()
    
    # Use proprietary algorithms
    result = await engine.optimize({
        'type': 'ml_model',
        'framework': 'pytorch',
        'optimization_level': 'maximum'
    })
    
    print(f"Achieved {result.improvement}% improvement")

asyncio.run(main())
```

### Plugin Development Example

```python
# plugin.json
{
    "name": "custom-db-optimizer",
    "version": "1.0.0",
    "author": "Your Company",
    "description": "Custom database optimization plugin",
    "class_name": "CustomDBOptimizer",
    "plugin_type": "optimizer",
    "license_model": "proprietary",
    "price": 99.99,
    "dependencies": ["uaengine-core>=1.0.0"],
    "checksum": "sha256:..."
}

# main.py
from uaengine.plugins import ProprietaryPlugin
from uaengine.plugins import PluginMetadata, PluginType

class CustomDBOptimizer(ProprietaryPlugin):
    async def initialize(self, config):
        self.optimization_level = config.get('level', 'standard')
    
    async def _execute_proprietary(self, target):
        # Your proprietary optimization logic
        improvements = await self._analyze_queries(target)
        return {
            'improvement': improvements,
            'optimized_queries': self._optimized_queries
        }
    
    def get_capabilities(self):
        return {
            'databases': ['postgresql', 'mysql', 'mongodb'],
            'optimization_types': ['query', 'index', 'schema'],
            'max_improvement': 300  # 300% improvement possible
        }
```

## Security & Compliance

### Plugin Security
- All plugins are sandboxed by default
- Proprietary plugins require signed certificates
- Checksum verification on all plugin loads

### Export Compliance
- Some algorithms may have export restrictions
- Check plugin metadata for restrictions
- Enterprise features may be restricted in certain countries

## Revenue Sharing for Plugin Developers

If you develop proprietary plugins:
- 70% revenue share to developers
- 30% to UAEngine for marketplace and infrastructure
- Automated license key generation and validation
- Built-in usage tracking and analytics

## Getting Help

- Documentation: https://docs.uaengine.org
- Community: https://community.uaengine.org
- Commercial Support: support@uaengine.org
- Legal Questions: legal@uaengine.org

