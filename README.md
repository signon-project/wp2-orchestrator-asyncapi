# SignON AsyncAPI
The SignON Orchestrator AsyncAPI repository is part of [SignON](https://signon-project.eu/) an EU H2020 research and innovation funded project.  
This repository specifies the how the [SignON Orchestrator](https://github.com/signon-project/wp2-orchestrator) communicates internally with the SignON Pipeline components through a message broker ([RabbitMQ](https://www.rabbitmq.com/)).

For further details please refer to public deliverable [D2.4 - Intermediate release of the Open SignON Framework](https://signon-project.eu/publications/public-deliverables/).

## Getting Started
To generate the SignON Orchestrator AsyncAPI documentation, please follow the following steps.

### Prerequisites
- NVM:
```curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash ```
- Node and NPM:
```nvm install 14```

### Installation
- AsyncAPI Generator:
```npm install -g @asyncapi/generator```

- AsyncAPI HTML Template:
```npm install -g @asyncapi/html-template```

- AsyncAPI Markdown Template:
```npm install -g @asyncapi/markdown-template```

### Usage
- Generate Documentation:
Start the Script from the root folder of this repository with:
```. asyncapi_docgen.sh```

## Additional information

### Compatibility Matrix

| SignON Orchestrator AsyncAPI | SignON Orchestrator Shared Schemas |
|:----------------------------:|:-------------------:|
|        8.0                   |         6.1         |

### Documentation
The generated documentation can be found in `docs` folder.  
It is provided in two formats:
- [HTML](docs/html/index.html)
- [Markdown](docs/markdown/asyncapi.md)

### Guideline for API styles
In order to standardize the AsyncAPI names for messages, components and fields the official guide from AsyncAPI has been followed [link](https://www.asyncapi.com/docs/reference/specification/v2.2.0).

Some of the most important rules are:
 - Messages names are in Camel Case with the first letter in upper case
 - Components names are in Camel Case with the first letter in upper case
 - Fields names are in Camel Case with the first letter in lower case
 
#### Other details
- IDE: Visual Studio Code

## Authors
This project was developed by [FINCONS GROUP AG](https://www.finconsgroup.com/) within the Horizon 2020 European project SignON under grant agreement no. [101017255](https://doi.org/10.3030/101017255).  
For any further information, please send an email to [signon-dev@finconsgroup.com](mailto:signon-dev@finconsgroup.com).

## License
This project is released under the [Apache 2.0 license](https://www.apache.org/licenses/LICENSE-2.0.html).