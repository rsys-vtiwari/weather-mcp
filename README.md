# Weather MCP Server

An MCP server that provides:

* Active US National Weather Service (NWS) alerts by two-letter state code
* Short-term point forecasts (next 5 periods) for latitude/longitude coordinates

Data is sourced from the public NWS API at https://api.weather.gov.

## Tools

| Tool | Description | Inputs |
|------|-------------|--------|
| `get_alerts` | Fetch active NWS alerts for a US state | `state` (string, two-letter code) |
| `get_forecast` | Fetch short-term forecast (next 5 periods) for coordinates | `latitude` (number), `longitude` (number) |

## Usage (Local)

Install dependencies:

```powershell
pip install .
```

Run the MCP server (stdio transport):

```powershell
python -m weather.weather
```

Your MCP client should be configured to launch the server via the package entrypoint or the above module path.

## Server JSON Summary

See `server.json` for registry metadata including name, version, tools, and entrypoint configuration.

## Publishing Steps (Overview)

1. Authenticate with publisher (GitHub namespace):
	```powershell
	mcp-publisher login github
	```
2. Create and push repo to GitHub (see steps below).
3. (Optional) Publish to PyPI if distributing as a package.
4. Publish to MCP registry:
	```powershell
	mcp-publisher publish
	```
5. Verify:
	```powershell
	curl "https://registry.modelcontextprotocol.io/v0/servers?search=io.github.vtiwari/weather-mcp"
	```

## Create & Push GitHub Repository

If this directory is not yet a git repo:

```powershell
git init
git add .
git commit -m "Initial commit: Weather MCP server"
```

Create repo (GitHub CLI) and push:

```powershell
gh repo create vtiwari/weather-mcp --public --source . --remote origin --push
```

If not using GitHub CLI, create the repo manually via the GitHub web UI, then:

```powershell
git remote add origin https://github.com/vtiwari/weather-mcp.git
git branch -M main
git push -u origin main
```

Tag version for release consistency:

```powershell
git tag v0.1.0
git push origin v0.1.0
```

## PyPI Packaging (Optional)

To distribute via PyPI, ensure `pyproject.toml` includes build backend and metadata (authors, license). Then:

```powershell
pip install build twine
python -m build
twine upload dist/*
```

## License

MIT (adjust if different).

## Disclaimer

This server uses public NOAA/NWS endpoints. Respect API usage guidelines and rate limits.

