FROM python:3.12-slim AS builder
WORKDIR /app
COPY worker/requirements.txt .
RUN pip3 install --user --upgrade pip && pip3 install --user -r requirements.txt

FROM python:3.12-slim
WORKDIR /app
RUN useradd -m appuser
USER appuser
COPY --from=builder /root/.local /home/appuser/.local
ENV PATH=/home/appuser/.local/bin:$PATH
COPY worker/ .
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
  CMD python3 worker.py --healthcheck || exit 1
CMD ["python3", "worker.py"]
