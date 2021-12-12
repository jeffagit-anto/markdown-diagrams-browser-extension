# Markdown Diagrams <small>(browser extension)</small>

A browser extension for Chrome, Edge, Opera and Firefox that renders markdown diagrams and charts code blocks into preview images.

## Supports many languages
[PlantUML](https://plantuml.com/), [Mermaid](https://mermaid-js.github.io/mermaid), [C4 with PlantUML](https://github.com/RicardoNiepel/C4-PlantUML), [GraphViz](https://www.graphviz.org), [Erd](https://github.com/BurntSushi/erd), [Nomnoml](http://www.nomnoml.com), [BPMN](https://bpmn.io), [BlockDiag](http://blockdiag.com), [SeqDiag](http://blockdiag.com/en/seqdiag), [ActDiag](http://blockdiag.com/en/actdiag), [NwDiag](http://blockdiag.com/en/nwdiag), [PacketDiag](http://blockdiag.com/en/nwdiag/packetdiag-examples.html), [RackDiag](http://blockdiag.com/en/nwdiag/rackdiag-examples.html), [Bytefield](https://github.com/Deep-Symmetry/bytefield-svg), [Ditaa](http://ditaa.sourceforge.net), [Svgbob](https://ivanceras.github.io/svgbob-editor), [UMlet](http://www.itmeyer.at/umlet/uml2), [Vega](https://vega.github.io/vega), [Vega-Lite](https://vega.github.io/vega-lite), [WaveDrom](https://wavedrom.com).

## Supports any website
- **GitHub** ([demo](https://github.com/marcozaccari/markdown-diagrams-browser-extension/tree/master/doc/examples)), **GitLab** ([demo](https://gitlab.com/markzackie/markdown-diagrams-browser-extension/-/tree/master/doc/examples)), **Bitbucket** ([demo](https://bitbucket.org/marcozaccari2/markdown-diagrams-browser-extension/src/master/doc/examples)): markdown files, pull requests, issues description, gists, wiki...
- **Atlassian**: Jira, Confluence, Trello...
- **all other websites** trying known patterns.
- **local files** when rendered with some markdown extension (for example [this](https://chrome.google.com/webstore/detail/markdown-preview-plus/febilkbfcbhebfnokafefeacimjdckgl)).

## Install

- <img height="16" src="https://upload.wikimedia.org/wikipedia/commons/a/a5/Google_Chrome_icon_%28September_2014%29.svg"> **Google Chrome**: [Markdown Diagrams - Chrome Web Store](https://chrome.google.com/webstore/detail/markdown-diagrams/pmoglnmodacnbbofbgcagndelmgaclel)
- <img height="16" src="https://upload.wikimedia.org/wikipedia/commons/a/a0/Firefox_logo%2C_2019.svg"> **Firefox**: [Markdown Diagrams - Firefox Add-ons](https://addons.mozilla.org/en-GB/firefox/addon/markdown-diagrams)
- <img height="16" src="https://upload.wikimedia.org/wikipedia/it/9/98/Microsoft_Edge_logo_%282019%29.svg"> **Edge**: [Markdown Diagrams - Edge Add-ons](https://microsoftedge.microsoft.com/addons/detail/markdown-diagrams/hceenoomhhdkjjijnmlclkpenkapfihe)
- <img height="16" src="https://upload.wikimedia.org/wikipedia/commons/4/49/Opera_2015_icon.svg"> **Opera**: [Markdown Diagrams - Opera Addons](https://addons.opera.com/it/extensions/details/markdown-diagrams)


## How to use

Simply put diagram or chart code into a blockquote:
````markdown
```language

code here

```
````

Double click to rendered diagram to swith to code/diagram. 
Click to extension icon to disable/enable parsing in current browser tab.

## Examples
plantuml with includes
```plantuml
@startuml

'!include styles.plantuml
!include https://raw.githubusercontent.com/inthepocket/plantuml-styles/master/styles.plantuml

actor "Resource Owner" as USER
participant "Client" as CLIENT
participant "Authorization Server" as AUTH
participant "Resource Server" as API

== OAuth 2.0 Authorization Code Grant ==
ref over USER, CLIENT: Some reference
USER -> CLIENT: Authenticate
activate CLIENT
CLIENT --> USER: Redirect to \n/authorize?response_type=code&client_id=<&x>&redirect_uri=<&x>&scope=<&x>
deactivate CLIENT
USER -> AUTH: GET /authorize?response_type=code&client_id=<&x>&redirect_uri=<&x>&scope=<&x>
activate AUTH
USER -> AUTH: Provide credentials
USER -> AUTH: Approve scope
AUTH --> USER: Redirect to \n<b>redirect_uri</b>?code=<&x>
deactivate AUTH
USER -> CLIENT: GET <b>redirect_uri</b>?code=<&x>
activate CLIENT
CLIENT -> AUTH: POST /token \ngrant_type=authorization_code\ncode=<&x>\nredirect_uri=<&x>\nclient_id=<&x>
activate AUTH
AUTH -> AUTH: Validate authorization_code,\n redirect_uri and client_id
AUTH --> CLIENT: access_token=<&x>\ntoken_type=\nexpires_in=3600\nrefresh_token=<&x>
deactivate AUTH
alt Authorization code OK
CLIENT --> USER: 200 OK
else Authorization code expired
CLIENT --> USER: 401 Not Authorized
end
deactivate CLIENT

... Some delay ...

== OAuth 2.0 Resource Request ==

USER -> CLIENT: Request resource
activate CLIENT
CLIENT -> API: GET /resource\nAuthorization: Bearer <b>access_token</b>
activate API
API -> API: Validate access_token
API --> CLIENT: resource
deactivate API
CLIENT --> USER: resource
deactivate CLIENT


== OAuth 2.0 Refreshing an Access Token ==


CLIENT -> AUTH: POST /token \ngrant_type=refresh_token\nrefresh_token=<&x>\nscope=<&x>
activate CLIENT
activate AUTH
AUTH -> AUTH: Validate refresh_token
AUTH --> CLIENT: access_token=<&x>\ntoken_type=\nexpires_in=3600\nrefresh_token=<&x>
deactivate AUTH
deactivate CLIENT

@enduml

    ```

Diagrams and charts code examples [here](doc/examples) and [here](https://kroki.io/examples.html).

![Diagram example](https://kroki.io/plantuml/svg/eJxNjrEOwjAMRHd_hZUJkPoLVTswMMNWdYiK01hKE5S4C1-Po2RgsvXufOepiM1yHgEutysOw4jmEVnYBv5a4RQNADs0z3QQvqiIQfEUAat3kXzS2sV5a3ZsKXNMasz_OPPuRTVtAgqFKhsXZ3XtIeI57li1nrPc47uiT04blbK2W2UOYNKpj_8Ace07KA==)
<details>
    <summary>Show code</summary>

    ```plantuml
    @startuml
    (*) --> "Initialization"

    if "Some Test" then
    -->[true] "Some Action"
    --> "Another Action"
    -right-> (*)
    else
    ->[false] "Something else"
    -->[Ending process] (*)
    endif

    @enduml
    ```
</details>

![Chart example](https://kroki.io/mermaid/svg/eJwryEzlUnLJTy9WUrBSMLYw41JyTiwBcyxMuZSCoGxDUwDShQm9)
<details>
    <summary>Show code</summary>

    ```mermaid
    pie
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
    ```
</details>


#### Special thanks

Some work derived from https://github.com/dai0304/pegmatite and https://github.com/asciidoctor/asciidoctor-browser-extension.
