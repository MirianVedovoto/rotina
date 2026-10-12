# Rotina Leve — gerar APK Android pelo GitHub Actions

## Estrutura importante
Envie o conteúdo desta pasta para a raiz do repositório GitHub. A pasta `.github/workflows/` precisa permanecer com esse nome (incluindo o ponto inicial), pois é onde o GitHub procura os workflows.

## Como gerar o APK
1. Envie o conteúdo desta pasta para a raiz do repositório, incluindo `www/`, `package.json`, `capacitor.config.json` e `.github/workflows/build-apk.yml`.
2. No GitHub, abra a aba **Actions** e habilite os workflows, se for solicitado.
3. Selecione **Gerar APK Android** e clique em **Run workflow**. Um push para `main` ou `master` também inicia a compilação.
4. Quando a execução terminar com um visto verde, abra a execução e baixe o artefato **rotina-leve-apk**.
5. Extraia o ZIP baixado e instale `app-debug.apk` no Android. Talvez seja necessário permitir a instalação de apps dessa fonte nas configurações do Android.

## Correções feitas
- Workflow em `.github/workflows/`, caminho exigido pelo GitHub Actions.
- Incluído `package-lock.json`; o workflow usa `npm ci` (instalação reproduzível) e cache do npm.
- Instalação explícita de `platforms;android-35` e `build-tools;35.0.0`, exigidos pelo Capacitor 7.
- `.gitignore` para não subir `node_modules/`, `android/` e APKs.
- `adjustMarginsForEdgeToEdge: force` no Capacitor, para o cabeçalho não ficar embaixo da barra de status no Android 15.
- Exportar backup agora funciona no APK (via plugins Filesystem + Share); o download por blob não funciona no WebView.
- Service worker desativado dentro do APK; recarrega o app na virada do dia; erro de gravação no armazenamento é avisado.

## Observações
Este fluxo gera um APK **debug/de teste**, não um APK de release assinado para publicação na Google Play. O app salva os dados localmente; desinstalar ou limpar os dados pode apagá-los. Os horários configurados atualmente são apenas preferências: alarmes e notificações nativas ainda não foram implementados.
