# Homework 5 — Deploying Machine Learning Models

Frozen lead-scoring model (`DictVectorizer` + `LogisticRegression`) from the
[2026 cohort release](https://github.com/DataTalksClub/machine-learning-zoomcamp/tree/master/cohorts/2026/homework/05-deployment),
served with FastAPI and packaged with Docker. The release files (`model.py`,
`predict.py`, `train.py`, `pipeline.bin`, `Dockerfile`, `uv.lock`, ...) are copied
unchanged. My own script for Q3 is `q3_predict.py`.

```bash
sha256sum pipeline.bin   # 1646bbdc...29f1, matches model_metadata.json
uv sync --locked
uv run python smoke_test.py
uv run python q3_predict.py
uv run uvicorn predict:app --host 0.0.0.0 --port 9696   # then: uv run python q6_test.py

docker build -t zoomcamp-model:2026-hw5 .
docker run --rm -p 9696:9696 zoomcamp-model:2026-hw5    # then: uv run python q6_test.py
```

## Answers

| Q | Answer | How |
| --- | --- | --- |
| 1 | `uv 0.12.13` | `uv --version` (setup check, not graded) |
| 2 | `1.7.2` | scikit-learn version in `pyproject.toml` / `uv.lock` |
| 3 | **0.533** | `q3_predict.py`, `pickle.load` + `predict_proba` |
| 4 | **0.770** | `POST /predict` on the local uvicorn server (0.769799) |
| 5 | `python:3.11.15-slim-bookworm` | `FROM` line of the `Dockerfile` |
| 6 | **0.770** | same request against the container (0.769799) |

`GET /health` returns `{"status":"ok"}` with `model_sha256` equal to the one
in `model_metadata.json`, both locally and in the container.
