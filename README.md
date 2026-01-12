# Minería de Datos - ITAM 2025

Course materials for Data Mining at ITAM.

## Quick Start

### Prerequisites

- [uv](https://docs.astral.sh/uv/) - Python package manager
- [Just](https://just.systems/) - Command runner
- [Quarto](https://quarto.org/) - Scientific publishing system
- Python 3.13+

### Setup

```bash
# Install dependencies
just setup

# Start preview server
just preview
```

## Available Commands

Run `just` to see all available commands:

```bash
just install        # Install dependencies
just preview        # Preview the book locally
just render         # Build production site
just format         # Format code
just lint           # Check code quality
just fix            # Fix linting issues automatically
just lab            # Launch Jupyter Lab
just notebook       # Launch Jupyter Notebook
just clean          # Clean generated files
just pre-commit     # Run pre-commit hooks
just build          # Full build pipeline (format, lint, render)
```

## Development

### With VS Code DevContainers

1. Install "Dev Containers" extension
2. Open folder in VS Code
3. "Reopen in Container"
4. Everything is pre-configured!

### With GitHub Codespaces

Click "Code" → "Create codespace on main"

### Local Development

```bash
# Install uv (if not already installed)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Install Just (if not already installed)
curl --proto '=https' --tlsv1.2 -sSf https://just.systems/install.sh | bash -s -- --to ~/.local/bin

# Install Quarto
# macOS
brew install quarto

# Linux
wget https://github.com/quarto-dev/quarto-cli/releases/download/v1.6.39/quarto-1.6.39-linux-amd64.deb
sudo dpkg -i quarto-1.6.39-linux-amd64.deb

# Clone and setup
git clone https://github.com/YOUR_USERNAME/mineria_datos_itam.git
cd mineria_datos_itam
just setup
```

## Project Structure

```
.
├── .github/          # CI/CD workflows
│   └── workflows/
│       └── quarto-publish.yml
├── .devcontainer/    # VS Code devcontainer configuration
├── chapters/         # Quarto book content (.qmd files)
│   ├── _quarto.yml   # Quarto configuration
│   ├── index.qmd     # Book homepage
│   ├── 00-*.qmd      # Requirements and setup
│   ├── 01-*.qmd      # Introduction
│   ├── 02-*.qmd      # Principles
│   ├── 03-*.qmd      # Linear regression
│   ├── 04-*.qmd      # Classification
│   ├── 05-*.qmd      # Trees
│   └── 06-*.qmd      # Boosting
├── notebooks/        # Jupyter notebooks (examples & exercises)
│   ├── introduccion.ipynb
│   ├── regresion_lineal.ipynb
│   ├── california_housing_case_study.ipynb
│   └── ...
├── docs/             # Generated site (auto-built by CI)
├── tareas/           # Student assignments
├── pyproject.toml    # Python dependencies
├── uv.lock           # Locked dependencies
├── justfile          # Command definitions
└── .pre-commit-config.yaml  # Pre-commit hooks
```

## Course Content

1. **Requerimientos y Computación** - Prerequisites and setup
2. **Introducción** - Introduction to data mining
3. **Principios** - Fundamental principles
4. **Regresión Lineal** - Linear regression concepts and applications
5. **Clasificación** - Classification techniques
6. **Árboles de Decisión** - Decision trees and ensemble methods
7. **Boosting** - Advanced boosting algorithms (XGBoost, LightGBM, CatBoost)

## Contributing

1. Create a feature branch
2. Make changes
3. Run `just format` and `just lint`
4. Commit changes (pre-commit hooks will run automatically)
5. Push and create PR

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

## Technology Stack

- **Python 3.13** - Latest stable Python
- **uv** - Fast Python package manager (replaces conda/pip)
- **Quarto** - Scientific publishing system
- **Just** - Modern command runner
- **Ruff** - Fast Python linter and formatter
- **Pre-commit** - Git hooks for code quality

### Key Libraries

- **Data Science**: NumPy, Pandas, Matplotlib, Seaborn
- **Machine Learning**: scikit-learn
- **Gradient Boosting**: XGBoost, LightGBM, CatBoost
- **Notebooks**: Jupyter, JupyterLab

## Automated Publishing

The course website is automatically rendered and published to GitHub Pages on every push to the main branch. The CI/CD pipeline:

1. Installs Python 3.13 and uv
2. Installs all dependencies
3. Renders the Quarto book
4. Deploys to GitHub Pages

## License

MIT License - see LICENSE file for details.

## Contact

For questions or issues, please open an issue on GitHub.
