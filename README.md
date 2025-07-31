# NetEnv - Netlify Environment Variable Uploader

A command-line tool to upload environment variables from `.env` files to Netlify projects.

## Features

- 📁 Read environment variables from `.env` files
- 🚀 Upload variables to Netlify projects automatically
- 🔍 Find projects by name (case-insensitive)
- 🔄 Update existing variables or create new ones
- 🛡️ Dry-run mode to preview changes
- 🎨 Beautiful CLI interface with progress indicators
- 📦 Packaged as a Windows executable

## Installation

### Option 1: Build from source

1. Clone this repository:
```bash
git clone <repository-url>
cd netenv
```

2. Install dependencies:
```bash
npm install
```

3. Build the executable:
```bash
npm run build
```

4. Add the executable to your PATH or move it to a directory in your PATH.

### Option 2: Install globally (if published to npm)

```bash
npm install -g netenv
```

## Setup

1. Get your Netlify API token:
   - Go to https://app.netlify.com/user/applications#personal-access-tokens
   - Create a new personal access token
   - Copy the token

2. Set the token as an environment variable (recommended):
   ```powershell
   $env:NETLIFY_TOKEN="your-token-here"
   ```

   Or add it to your PowerShell profile for persistence:
   ```powershell
   Add-Content $PROFILE '$env:NETLIFY_TOKEN="your-token-here"'
   ```

## Usage

### Basic Usage

Navigate to your project directory and run:

```bash
netenv
```

This will:
- Use the current directory name as the project name
- Read from `.env` file in the current directory
- Upload all environment variables to Netlify

### Advanced Usage

```bash
# Specify a different project name
netenv --project my-awesome-project

# Use a different .env file
netenv --file .env.production

# Provide token via command line
netenv --token your-token-here

# Dry run (preview without uploading)
netenv --dry-run

# Combine options
netenv --project my-project --file .env.staging --dry-run
```

### Command Line Options

| Option | Description | Default |
|--------|-------------|---------|
| `-p, --project <name>` | Netlify project name | Current directory name |
| `-f, --file <path>` | Path to .env file | `.env` |
| `-t, --token <token>` | Netlify API token | `NETLIFY_TOKEN` env var |
| `-d, --dry-run` | Preview changes without uploading | `false` |
| `-h, --help` | Show help | - |
| `-V, --version` | Show version | - |

## Example Workflow

1. **Create a new project:**
   ```bash
   mkdir my-new-project
   cd my-new-project
   ```

2. **Create a .env file:**
   ```bash
   # .env
   DATABASE_URL=postgresql://user:pass@localhost:5432/db
   API_KEY=your-secret-api-key
   NODE_ENV=production
   ```

3. **Deploy to Netlify:**
   - Push your code to GitHub/GitLab
   - Connect the repository to Netlify
   - Deploy the site

4. **Upload environment variables:**
   ```bash
   netenv
   ```

   Or if your Netlify site has a different name:
   ```bash
   netenv --project my-netlify-site-name
   ```

## .env File Format

The tool supports standard `.env` file format:

```bash
# Comments are ignored
DATABASE_URL=postgresql://user:pass@localhost:5432/db
API_KEY=your-secret-key
NODE_ENV=production

# Values can be quoted
SECRET_KEY="my-secret-value"
MESSAGE='Hello World'

# Empty lines are ignored
```

## Error Handling

The tool provides clear error messages for common issues:

- **Missing .env file**: Shows the expected path and suggests creating one
- **Missing API token**: Provides instructions on how to get and set the token
- **Site not found**: Suggests checking the project name
- **API errors**: Shows detailed error information from Netlify

## Security

- Environment variable values are masked in the output for security
- API tokens should be stored as environment variables, not in code
- The tool only uploads variables from your local `.env` file

## Troubleshooting

### "Site not found" error
- Make sure your site is deployed on Netlify
- Check that the project name matches your Netlify site name
- Use `--project` flag to specify the exact site name

### "API token required" error
- Set the `NETLIFY_TOKEN` environment variable
- Or use the `--token` flag
- Get your token from https://app.netlify.com/user/applications#personal-access-tokens

### "Permission denied" error
- Make sure your API token has the necessary permissions
- Check that you own the site or have admin access

## Development

### Running from source

```bash
npm start
```

### Testing

```bash
# Test with dry run
npm start -- --dry-run

# Test with specific project
npm start -- --project test-project --dry-run
```

## License

MIT License - see LICENSE file for details. 