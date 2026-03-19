![Platforms](https://img.shields.io/badge/platform-Windows|MacOS-lightgray.svg)
![.NET](https://img.shields.io/badge/.NET%20-8-blue.svg)
[![License](http://img.shields.io/:license-MIT-blue.svg)](http://opensource.org/licenses/MIT)
[![oAuth2](https://img.shields.io/badge/oAuth2-v1-green.svg)](http://developer.autodesk.com/)
[![Data-Management](https://img.shields.io/badge/Data%20Management-v2-green.svg)](http://developer.autodesk.com/)
[![AEC-Data-Model](https://img.shields.io/badge/AEC%20Data%20Model-v1-green.svg)](http://developer.autodesk.com/)

# aps-aecdm-mcp-dotnet
.NET MCP Server to connect with Claude Desktop, AEC Data Model API and the Viewer.

## Introduction

This sample started as an experiment with the new [Model Context Protocol](https://modelcontextprotocol.io/introduction) brought as a challenge during one of our [Autodesk Platform Accelerators](https://aps.autodesk.com/accelerator-program). Special thanks to [Mirco Bianchini](https://www.linkedin.com/in/mirco-bianchini-352b2128/) for bringing this challenge and contributing to get to the solutions presented in this repo.


## Prerequisites

To make this work, you'll need to:

- Download and Install [Claude Desktop](https://claude.ai/download)
- Clone or download this repo
- Build this project
- Add a reference to the .csproj in the Claude configuration file (developers resource)

## [DEMO VIDEO HERE](https://youtu.be/GlCYJQfUFWU)

## How it works

This sample creates an MCP server using the [ModelContextProtocol .NET SDK](https://www.nuget.org/packages/ModelContextProtocol/0.1.0-preview.6).

In this scope we added 4 main tools to our server:

1. [GetToken](https://github.com/JoaoMartins-callmeJohn/aps-aecdm-mcp-dotnet/blob/main/mcp-server-aecdm/AuthTools.cs#L18-L21) to obtain a PKCE token that is used in the APS API requests.
2. [GetHubs](https://github.com/JoaoMartins-callmeJohn/aps-aecdm-mcp-dotnet/blob/main/mcp-server-aecdm/AECDMTools.cs#L28-L52) to retrieve the hubs using the AEC Data Model API
3. [GetProjects](https://github.com/JoaoMartins-callmeJohn/aps-aecdm-mcp-dotnet/blob/main/mcp-server-aecdm/AECDMTools.cs#L55-L83) to retrieve the projects using the AEC Data Model API
4. [GetElementGroupsByProject](https://github.com/JoaoMartins-callmeJohn/aps-aecdm-mcp-dotnet/blob/main/mcp-server-aecdm/AECDMTools.cs#L86-L131) to retrieve the ElementGroups using the AEC Data Model API
5. [GetElementsByElementGroupWithCategoryFilter](https://github.com/JoaoMartins-callmeJohn/aps-aecdm-mcp-dotnet/blob/main/mcp-server-aecdm/AECDMTools.cs#L134-L200) to retrieve the elements from one ElementGroup using a category filter.
6. [RenderModel](https://github.com/JoaoMartins-callmeJohn/aps-aecdm-mcp-dotnet/blob/main/mcp-server-aecdm/ViewerTool.cs#L32C36-L143) to render one design with the Viewer
7. [HighLightElements](https://github.com/JoaoMartins-callmeJohn/aps-aecdm-mcp-dotnet/blob/main/mcp-server-aecdm/ViewerTool.cs#L21-L29) to highlight elements in the Viewer.

With these tools, you can use natural language to query the data from your elementgroups using the AEC Data Model API.

This is a first experiment with this new protocol. Feel free to submit suggestions and collaborate to this repo so we can improve its functionalities.

# Setup

## Running locally

Clone this project or download it. It's recommended to install [GitHub desktop](https://desktop.github.com/). To clone it via command line, use the following (**Terminal** on MacOSX/Linux, **Git Shell** on Windows):

    git clone https://github.com/joaomartins-callmejohn/aps-aecdm-mcp-dotnet

**Visual Studio** (Windows):

Replace **client_id** with your own key (Single Page application).
You can do it directly in the 'Properties/lauchSettings.json' file or through Visual Studio UI under the debug properties.

You'll need to add a reference to your MCP server in the `claude_desktop_congif.json` file
```json
{
    "mcpServers": {
      "aecdm": {
            "command": "dotnet",
            "args": [
                "run",
                "--project",
                "C:\\Users\\...mcp-server-aecdm.csproj",
                "--no-build"
            ]
        }
    }
}
```

# Further Reading

### Troubleshooting

1. **Can't find my hub**: [Provision your APS app in your hub of Forma for Construction](https://get-started.aps.autodesk.com/#provision-access-in-other-products)

2. If you made changes to the code and want this to be reflected in Claude, you'll need to end the CLaude task before rebuilding the solution.

## License

This sample is licensed under the terms of the [MIT License](http://opensource.org/licenses/MIT). Please see the [LICENSE](LICENSE) file for full details.

## Written by

João Martins [in/jpornelas](https://linkedin.com/in/jpornelas)
