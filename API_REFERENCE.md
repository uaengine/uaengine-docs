# API Reference

## Core Functions

### accelerate_platform(config=None)
Drop-in optimization function.

**Parameters:**
- config (dict, optional): Configuration override

**Returns:**
- dict: Performance report

### get_acceleration_opportunities(config=None)
Analyze without optimizing.

**Returns:**
- dict: Optimization opportunities

## UniversalAccelerationEngine Class

### Methods

- `detect_platform()`: Auto-detect platform
- `discover_system()`: Find components
- `optimize_all()`: Apply optimizations
- `get_performance_report()`: Get metrics
- `stop_monitoring()`: Stop monitoring

## Configuration Schema

```json
{
  "engine": {
    "auto_optimize": true,
    "monitoring_enabled": true,
    "rollback_on_failure": true
  },
  "thresholds": {
    "max_cpu_percent": 80.0,
    "max_memory_percent": 85.0
  },
  "optimizations": {
    "database": {"enabled": true},
    "web_server": {"enabled": true},
    "file_system": {"enabled": true}
  }
}
```
