FROM ubuntu:22.04

# ==============================
# 必要なパッケージのインストール
# バージョンは2024/4/4時点で確認
# git           コード管理のため                        [version:2.34.1]
# curl          nodejs最新バージョンを取得するため
# sudo          管理者権限の実行が必要なときに使う
# nodejs        Nextjs開発環境構築のため                [version:20.12.0]
# typescript    Nextjs開発環境構築のため                [version:5.4.3]
# ==============================
RUN apt update && apt install -y \
    git \
    curl \
    sudo \
    && curl -fsSL https://deb.nodesource.com/setup_20.x | bash \
    && apt install -y nodejs \
    && npm install -g typescript@5.4.3
RUN npm install -g vercel@latest

# ==============================
# 開発用ユーザーを設定
ARG USERNAME=tcybar
ARG GROUPNAME=tcybar
ARG UID=1000
ARG GID=1000
RUN groupadd -g ${GID} ${GROUPNAME} && \
    useradd -m -s /bin/bash -u ${UID} -g ${GID} ${USERNAME}
RUN echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}
USER ${USERNAME}
# ==============================

# 作業ディレクトリの設定
WORKDIR /home/${USERNAME}/app

ENTRYPOINT ["/bin/bash"]