# Foundation Studio walkthrough

## What to demonstrate

Small executable examples reveal what frameworks actually do before adding a supervisor.

```powershell
uv run portfolio demo foundation
uv run --extra gradio python -m portfolio.gradio_app
```

### Follow the data

1. ChatPromptTemplate inserts question and optional history into typed messages.
2. RunnablePassthrough.assign preserves the original mapping and adds word_count.
3. RunnableBranch chooses a named response length based on its input contract.
4. RunnableParallel produces independent named results.
5. PydanticOutputParser parses and validates a JSON card; this is separate from asking a model to follow a schema.
6. Gradio renders incremental output. Demo chunks are explicitly generated from fixture text; live mode calls the configured model's stream interface.
7. Middleware wraps a real create_agent model step. HumanInTheLoopMiddleware pauses a proposed publication tool, then a Command resumes approval or rejection on the same saved thread.
8. Inspect effects_before_review and effects_after_review: approving records one simulated local effect, rejecting records zero. No online publication is performed.

Read [foundations.py](../src/portfolio/foundations.py), [gradio_app.py](../src/portfolio/gradio_app.py) and the [additional executable labs](../src/portfolio/labs.py).

### Practice questions

What is a runnable's input/output shape? What changes between invoke, batch, stream and ainvoke? Why can a schema-valid answer still be false? Why does a tool proposal need a matching ToolMessage? Why does saving chat history not automatically resume an interrupted graph? Why is a generated final sentence insufficient evidence that a tool actually executed?

### Additional experiments

Run `uv run python -m portfolio.labs` for sampling/cosine calculations, prompt/parser/LCEL execution, read-only owned SQL and checkpoint/state streaming examples. The labs are local and deterministic. Gmail OAuth, Tavily, PostgreSQL and trace exporters require explicit external credentials/setup; their extension exercises are documented rather than falsely reported as tested integrations.
