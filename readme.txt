# 環境構築手順

## 仮想環境構築
python -m venv myvenv

## 仮想環境実行
.\myvenv\Scripts\activate
## 仮想環境実行停止
deactivate

## requirements.txtを作成、入力
>開発に必要なパッケージとバージョンを記載する

## パッケージインストール
pip install -r requirements.txt

## djangoのプロジェクト作成
django-admin startproject mysite .

## ./mysite/settings.pyの修正
LANGUAGE_CODEをjaに変更
TIME_ZONEをAsia/Tokyoに変更

## DBセットアップ
python manage.py migrate

## webサーバー起動
python manage.py runserver
→URLに接続し、インストールの成功画面が表示されることを確認

## アプリケーション作成(appはアプリ名)
python manage.py startapp app

## アプリケーションの有効化
./mysite/settings.py を開き、INSTALLED_APPSに以下を追記(1つ目は必要時のみ)
    'widget_tweaks',
    'app',


## プロジェクトのルーティング設定
./mysite/urls.pyを開き、以下を修正

from django.urls import path
↓
from django.urls import path, include

urlpatterns に、以下を追記
    path('', include('app.urls')),

## アプリケーション用のルーティング設定
./app/urls.pyを作成し、以下を入力
from django.urls import path
from app import views

urlpatterns = [
  path('', views.IndexView.as_view(), name='index')
]

## formを作成(必要時)
./app/form.pyを作成し、以下を入力

## DB再構築(model修正等、必要時)
python manage.py makemigrations
python manage.py migrate