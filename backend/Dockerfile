FROM python:3.12-slim

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    POETRY_NO_INTERACTION=1 \
    POETRY_VIRTUALENVS_IN_PROJECT=1 \
    POETRY_VIRTUALENVS_CREATE=1 \
    POETRY_CACHE_DIR=/tmp/poetry_cache

WORKDIR /code

RUN apt-get update && apt-get install -y \
    libyaml-cpp-dev \
    libffi-dev \
    libglib2.0-0 \
    pango-1.0 \
    libcairo2 \
    locales \
    tzdata \
    gettext \
    fontconfig \
    fonts-freefont-ttf \
    zlib1g-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && locale-gen en_US.UTF-8 \
    && locale-gen ar_SA.UTF-8 \
    && locale-gen fr_FR.UTF-8 \
    && locale-gen pt_PT.UTF-8 \
    && locale-gen es_ES.UTF-8 \
    && locale-gen de_DE.UTF-8 \
    && locale-gen nl_NL.UTF-8 \
    && locale-gen it_IT.UTF-8 \
    && locale-gen pl_PL.UTF-8 \
    && locale-gen ro_RO.UTF-8 \
    && locale-gen hi_IN.UTF-8 \
    && locale-gen ur_PK.UTF-8 \
    && locale-gen cs_CZ.UTF-8 \
    && locale-gen sv_SE.UTF-8 \
    && locale-gen id_ID.UTF-8 \
    && pip install --no-cache-dir --upgrade pip poetry==2.0.1

COPY pyproject.toml poetry.lock ./

RUN poetry install --no-root \
    && rm -rf $POETRY_CACHE_DIR

#watch out for local files during dev and maintenance of .dockerignore
COPY . .

EXPOSE 8000
ENTRYPOINT ["poetry", "run", "bash", "startup.sh"]
