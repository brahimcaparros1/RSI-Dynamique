# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

RSI Dynamique is a professional Pine Script v6 indicator for TradingView that implements a dynamic RSI with adaptive zones based on ATR volatility. The project follows TDD (Test-Driven Development) methodology with comprehensive testing framework.

## Core Architecture

### Main Components
- **rsi_dynamique.pine**: Main indicator with dynamic zones, multi-timeframe analysis, divergence detection, and integrated backtesting
- **test_rsi_dynamique.pine**: Comprehensive test suite with unit, integration, and performance tests
- **docs/**: Performance metrics and API reference documentation
- **examples/**: Trading strategy configurations for different market types

### Key Technical Features
- Dynamic overbought/oversold zones: `70 ± (ATR_normalized × volatility_factor)`  
- EMA-smoothed RSI with configurable periods
- Real-time statistics dashboard with success rates and drawdown tracking
- Alert system with divergence detection
- Multi-timeframe support with higher timeframe analysis

## Development Workflow

### Testing and Validation
```pinescript
// Run tests by loading test_rsi_dynamique.pine in TradingView
// Enable "Afficher Résultats Tests" to see test results in logs
// 90%+ function coverage with 22 automated test scenarios
```

### Pine Script v6 Specifics
- Uses `indicator()` without `timeframe` parameters (has side effects like tables/alerts)
- Timeframe inputs must use minute format: `"60"` not `"1H"` for request.security()
- Plot titles must be const strings, cannot use string concatenation with input variables
- No `linestyle` parameter in plot() function, use `style` instead

### Common Pine Script v6 Issues to Watch
- String concatenation in plot titles with input variables causes compilation errors
- Side effects (tables, alerts, drawings) prevent use of timeframe parameters in indicator()
- Multi-timeframe functions require proper timeframe format strings

### Market-Specific Configurations
- **Forex**: RSI 14, ATR 20, volatility factor 0.5
- **Crypto**: RSI 21, ATR 14, volatility factor 0.7, confirmation 3 bars
- **Scalping**: RSI 7, ATR 10, volatility factor 0.3

## File Structure and Dependencies

### Primary Files
- `rsi_dynamique.pine`: 400+ lines, includes all functionality from RSI calculation to backtesting
- `test_rsi_dynamique.pine`: Test framework with assertion functions and automated test execution

### Key Functions Architecture
- `validate_params()`: Input parameter validation with runtime error handling
- `calculate_rsi()`: Custom RSI implementation with proper gain/loss averaging
- `normalize_atr()`: ATR normalization for dynamic zone calculation
- Dashboard table creation uses Pine Script v6 table API with position-based layout

### Error Handling Patterns
The codebase implements robust error handling with parameter validation and boundary checking. All user inputs are validated with appropriate min/max ranges and error messages.