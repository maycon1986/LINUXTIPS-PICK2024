FROM cgr.dev/chainguard/python:latest-dev@sha256:5727408976bf17a1f034ead1bb6f9c145b392e3ffb4246c7e557680dc345f6ff as build
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt --user

FROM cgr.dev/chainguard/python:latest@sha256:a66be254adc25216a93a381b868d8ca68c0b56f489cd9c0d50d9707b49a8a0a4
WORKDIR /app
COPY --from=build /home/nonroot/.local/lib/python3.12/site-packages /home/nonroot/.local/lib/python3.12/site-packages
COPY --from=build /app /app
ENTRYPOINT ["python", "-m", "flask", "run", "--host=0.0.0.0"]