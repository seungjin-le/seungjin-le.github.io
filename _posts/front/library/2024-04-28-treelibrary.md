---
title: "[ Mac ] 디렉토리 구조 출력 패키지"
author: <author_id>
categories: [ Mac,  Homebrew]
tags: [ Mac, Homebrew]
math: true
toc: true
mermaid: true
image: /images/backgrounds/library.png
---

### tree
외주 개발이 막바지에 이르렀을 때 인수인계 문서를 작성해 문서화를 해야 합니다. 그런데 만들어둔 파일과 디렉토리가
많다 보니 이걸 하나하나 다 찾아서 문서에 작성하는 게 보통 일이 아닌지라 방법을 찾다 보니 `tree`라는 패키지를 찾게
되었고 이 패키지는 터미널이 바라보고 있는 디렉토리 기준으로 하위 디렉토리를 전부 출력해 줍니다.

### Install tree
먼저 `Homebrew`를 설치가 안되어있다면 설치하시고
`Homebrew`가 설치 되었다는 가정하예 `tree`패키지를 설치해 줍니다.

```shell
brew install tree
```

### tree 패키지 사용 해보기

#### 터미널에서 디렉토리 이동
- ![tree1](/images/postImages/front/library/tree1.png)

#### tree 명령어 실행
사용법이 너무 쉬운 게 터미널에 간단하게 `tree`라고 입력하시면 됩니다.
그러면 모든 디렉토리와 파일 개수까지 출력해 줍니다.

- ![tree2](/images/postImages/front/library/tree2.png)


```shell
.
├── BULLETIN.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── Dockerfile
├── LICENSE
├── README.md
├── autogpt
│   ├── __init__.py
│   ├── __main__.py
│   ├── agent
│   │   ├── __init__.py
│   │   ├── agent.py
│   │   └── agent_manager.py
│   ├── api_manager.py
│   ├── app.py
│   ├── chat.py
│   ├── cli.py
│   ├── commands
│   │   ├── __init__.py
│   │   ├── analyze_code.py
│   │   ├── audio_text.py
│   │   ├── command.py
│   │   ├── execute_code.py
│   │   ├── file_operations.py
│   │   ├── git_operations.py
│   │   ├── google_search.py
│   │   ├── image_gen.py
│   │   ├── improve_code.py
│   │   ├── times.py
│   │   ├── twitter.py
│   │   ├── web_playwright.py
│   │   ├── web_requests.py
│   │   ├── web_selenium.py
│   │   └── write_tests.py
│   ├── config
│   │   ├── __init__.py
│   │   ├── ai_config.py
│   │   └── config.py
│   ├── configurator.py
│   ├── js
│   │   └── overlay.js
│   ├── json_utils
│   │   ├── __init__.py
│   │   ├── json_fix_general.py
│   │   ├── json_fix_llm.py
│   │   ├── llm_response_format_1.json
│   │   └── utilities.py
│   ├── llm_utils.py
│   ├── logs.py
│   ├── main.py
│   ├── memory
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── local.py
│   │   ├── milvus.py
│   │   ├── no_memory.py
│   │   ├── pinecone.py
│   │   ├── redismem.py
│   │   └── weaviate.py
│   ├── models
│   │   └── base_open_ai_plugin.py
│   ├── modelsinfo.py
│   ├── plugins.py
│   ├── processing
│   │   ├── __init__.py
│   │   ├── html.py
│   │   └── text.py
│   ├── prompts
│   │   ├── __init__.py
│   │   ├── generator.py
│   │   └── prompt.py
│   ├── setup.py
│   ├── singleton.py
│   ├── speech
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── brian.py
│   │   ├── eleven_labs.py
│   │   ├── gtts.py
│   │   ├── macos_tts.py
│   │   └── say.py
│   ├── spinner.py
│   ├── token_counter.py
│   ├── types
│   │   └── openai.py
│   ├── url_utils
│   │   ├── __init__.py
│   │   └── validators.py
│   ├── utils.py
│   └── workspace
│       ├── __init__.py
│       └── workspace.py
├── azure.yaml.template
├── benchmark
│   ├── __init__.py
│   └── benchmark_entrepreneur_gpt_with_difficult_user.py
├── codecov.yml
├── data_ingestion.py
├── docker-compose.yml
├── docs
│   ├── code-of-conduct.md -> ../CODE_OF_CONDUCT.md
│   ├── configuration
│   │   ├── imagegen.md
│   │   ├── memory.md
│   │   ├── search.md
│   │   └── voice.md
│   ├── contributing.md -> ../CONTRIBUTING.md
│   ├── imgs
│   │   └── openai-api-key-billing-paid-account.png
│   ├── index.md
│   ├── plugins.md
│   ├── setup.md
│   ├── testing.md
│   └── usage.md
├── main.py
├── mkdocs.yml
├── plugin.png
├── plugins
│   └── __PUT_PLUGIN_ZIPS_HERE__
├── pyproject.toml
├── requirements.txt
├── run.bat
├── run.sh
├── run_continuous.bat
├── run_continuous.sh
├── scripts
│   ├── __init__.py
│   ├── check_requirements.py
│   └── install_plugin_deps.py
├── tests
│   ├── __init__.py
│   ├── browse_tests.py
│   ├── conftest.py
│   ├── context.py
│   ├── integration
│   │   ├── conftest.py
│   │   ├── goal_oriented
│   │   │   ├── cassettes
│   │   │   │   └── test_write_file
│   │   │   │       └── test_write_file.yaml
│   │   │   ├── goal_oriented_tasks.md
│   │   │   └── test_write_file.py
│   │   ├── memory_tests.py
│   │   ├── milvus_memory_tests.py
│   │   └── weaviate_memory_tests.py
│   ├── milvus_memory_test.py
│   ├── mocks
│   │   ├── __init__.py
│   │   └── mock_commands.py
│   ├── test_agent.py
│   ├── test_agent_manager.py
│   ├── test_api_manager.py
│   ├── test_commands.py
│   ├── test_config.py
│   ├── test_image_gen.py
│   ├── test_llm_utils.py
│   ├── test_local_cache.py
│   ├── test_prompt_generator.py
│   ├── test_token_counter.py
│   ├── test_utils.py
│   ├── test_workspace.py
│   ├── unit
│   │   ├── __init__.py
│   │   ├── _test_json_parser.py
│   │   ├── data
│   │   │   └── test_plugins
│   │   │       └── Auto-GPT-Plugin-Test-master.zip
│   │   ├── models
│   │   │   └── test_base_open_api_plugin.py
│   │   ├── test_browse_scrape_links.py
│   │   ├── test_browse_scrape_text.py
│   │   ├── test_chat.py
│   │   ├── test_commands.py
│   │   ├── test_file_operations.py
│   │   ├── test_get_self_feedback.py
│   │   ├── test_json_parser.py
│   │   ├── test_json_utils_llm.py
│   │   ├── test_plugins.py
│   │   ├── test_setup.py
│   │   └── test_spinner.py
│   ├── utils.py
│   └── vcr
│       └── openai_filter.py
└── tests.py

32 directories, 153 files
```

### 특정 디렉토리 제외하고 출력하기
출력하는 것까지는 좋지만 많은 라이브러리를 가지고 있는 `node_modules`같은 큰 디렉토리 나 개발자가 사용중인
`idea`의 셋팅값이 저장된 디렉토리인 `.idea`같이 인수인계 문서에는 필요없는 디렉토리를 제회 하고자 할때는 `tree`
의 명령어 뒤에 `-I {제외할 파일이나 디렉토리 이름}`을 추가하면 됩니다.
- #### ex) `tree -I node_modules -I .idea`
