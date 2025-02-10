FROM python:3.12-slim

RUN apt-get update -y

EXPOSE 8080

ARG USERNAME=python
ARG UID=1005
ARG GID=2000

RUN groupadd -g "${GID}" ${USERNAME} && useradd --create-home -u "${UID}" -g "${GID}" ${USERNAME}

USER ${USERNAME}

WORKDIR /home/${USERNAME}/services/backend

ENV PATH="$PATH:/home/${USERNAME}/.local/bin"
ENV PYTHONUNBUFFERED=1
ENV PYTHONDONTWRITEBYTECODE=1

COPY --chown=${USERNAME}:${USERNAME} ./services/backend/requirements.txt .

RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

COPY --chown=${USERNAME}:${USERNAME} ./services/backend .

RUN chmod +x ./scripts/docker-entrypoint.sh