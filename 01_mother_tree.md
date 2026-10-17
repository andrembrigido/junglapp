# MOTHER TREE — Padrão Árvore-Mãe
Versão 1.0 | Outubro/2026 | Flutter + Dart + GitHub + Supabase + Google OAuth

## Objetivo
Manual reproduzível para começar um aplicativo novo, sem depender de IA. Siga em ordem. Este é um MODELO; não reorganize o Butler existente. Filosofia Junglapp 2.0: mínimo de arquivos, responsabilidades claras, módulos autocontidos, simplicidade, escalabilidade, consistência e testes. No Butler, os padrões estão organizados em `00_junglapp/`. Em novos projetos, adapte a estrutura à sua necessidade.

## 1 — Preparar Windows
Instale Git for Windows, VS Code com extensões Flutter e Dart, Flutter SDK no PATH e Android Studio (Android SDK e um emulador com Google Play). Para compilar iOS, use um Mac com Xcode. Verifique no PowerShell:

    git --version
    flutter --version
    dart --version
    flutter doctor
    flutter doctor --android-licenses
    flutter devices

Corrija os avisos relevantes do flutter doctor. Reinicie o terminal se acabou de configurar o PATH.

## 2 — Pasta local
Exemplo em PowerShell (escolha seu próprio caminho):

    cd C:\Projetos
    mkdir meu_app
    cd meu_app
    code .

## 3 — GitHub
GitHub → New repository → nome meu_app → Private → deixe README, .gitignore e licença desmarcados → Create. Copie a URL HTTPS. Dentro da pasta local:

    git init
    git branch -M main
    git remote add origin https://github.com/SEU_USUARIO/meu_app.git
    git remote -v

Se o repositório remoto já tem arquivos/histórico, prefira clonar com git clone URL em vez de iniciar históricos separados.

## 4 — Quatro pastas padrão
Na RAIZ:

    mkdir 00_read, 01_data, 02_back, 03_front
    New-Item 00_read\README.md -ItemType File
    New-Item 02_back\README.md -ItemType File
    New-Item 01_data\README.md -ItemType File
    flutter create --project-name meu_app --platforms android,ios,web,windows 03_front

00_read: documentação e padrões. 01_data: migrações SQL, documentação, RLS (não é banco executável local). 02_back: reservado para servidor próprio apenas se necessário; Supabase já oferece backend. 03_front: Flutter/Dart. Não crie manualmente os diretórios android, ios, web e windows: flutter create gera os arquivos de plataforma. O Git não registra pastas vazias: deixe README ou .gitkeep.

Adicione .gitignore na raiz para ignorar **/.dart_tool/, **/build/, **/.gradle/, **/local.properties, **/.env, **/.env.*, *.jks, *.keystore, *.p8, arquivos de contas de serviço; preserve o .gitignore gerado no 03_front. Nunca versione senhas, service_role, client secrets ou chaves privadas.

## 5 — Estrutura Flutter
Dentro de 03_front/lib:

    main.dart            inicializa Flutter e serviços
    app.dart             MaterialApp e tema
    app_routes.dart      nomes e construção de rotas
    kolors.dart          cores compartilhadas
    responsive.dart      NOME PROVISÓRIO para responsividade
    pages/
      splash_page.dart
      login_page.dart
      home_page.dart

Dentro de 03_front/assets: images/, icons/, fonts/, audios/. Declare assets em pubspec.yaml somente quando houver arquivos. Nome responsive.dart NÃO é decisão final. Deve centralizar breakpoints e limites de largura para celular/tablet/desktop/TV; usar LayoutBuilder, MediaQuery, SafeArea, ConstrainedBox e rolagem quando necessário. Evitar larguras fixas que causem overflow.

Criar arquivos no PowerShell, a partir da raiz:

    mkdir 03_front\lib\pages
    New-Item 03_front\lib\app.dart, 03_front\lib\app_routes.dart, 03_front\lib\kolors.dart, 03_front\lib\responsive.dart -ItemType File
    New-Item 03_front\lib\pages\splash_page.dart, 03_front\lib\pages\login_page.dart, 03_front\lib\pages\home_page.dart -ItemType File

## 6 — Código inicial mínimo
Use estas responsabilidades para os arquivos; não misture navegação, cores e autenticação:
- main.dart: WidgetsFlutterBinding.ensureInitialized(); runApp(const MyApp());
- kolors.dart: classe Kolors com static const Color background, primary e text.
- responsive.dart: classe Responsive com MediaQuery.sizeOf(context).width e métodos isTablet (>=600), isDesktop (>=1024), contentMaxWidth (440 no celular, 720 desktop).
- app.dart: StatelessWidget MyApp que retorna MaterialApp(title, theme, initialRoute:'/', onGenerateRoute:AppRoutes.onGenerateRoute).
- app_routes.dart: AppRoutes com splash='/', login='/login', home='/home'; MaterialPageRoute para cada tela e fallback Splash.
- splash_page.dart: StatefulWidget, Future.delayed(Duration(seconds:2)), verifica mounted e chama Navigator.pushReplacementNamed(context,'/login').
- login_page.dart: Scaffold com botão provisório de teste que navega para '/home'. IDENTIFIQUE o botão como teste, NÃO como login real.
- home_page.dart: Scaffold, AppBar e botão para voltar a '/login'.

Modelo mínimo de main.dart antes do Supabase:

    import 'package:flutter/material.dart';
    import 'app.dart';
    void main() {
      WidgetsFlutterBinding.ensureInitialized();
      runApp(const MyApp());
    }

Modelo de app_routes.dart:

    import 'package:flutter/material.dart';
    import 'pages/splash_page.dart';
    import 'pages/login_page.dart';
    import 'pages/home_page.dart';
    abstract final class AppRoutes {
      static const splash = '/';
      static const login = '/login';
      static const home = '/home';
      static Route<dynamic> onGenerateRoute(RouteSettings s) {
        final Widget page = switch (s.name) {
          splash => const SplashPage(),
          login => const LoginPage(),
          home => const HomePage(),
          _ => const SplashPage(),
        };
        return MaterialPageRoute<void>(settings:s,builder:(_)=>page);
      }
    }

Teste a navegação ANTES de configurar login:

    cd 03_front
    flutter pub get
    flutter analyze
    flutter run

Com vários dispositivos: flutter run -d ID_DO_DISPOSITIVO. flutter run deve ser executado dentro de 03_front, não na raiz.

## 7 — Primeiro commit
Volte à raiz:

    cd ..
    git status
    git add .
    git commit -m "chore: initialize Mother Tree Flutter scaffold"
    git push -u origin main

Se pedir identidade: git config --global user.name "SEU NOME" e git config --global user.email "SEU_EMAIL".

## 8 — Criar Supabase
1. supabase.com/dashboard → New project → organização, nome, região e senha forte.
2. Project Settings/API (ou Connect) → anote Project URL e publishable key (sb_publishable_...).
3. Authentication → Providers → Google: configurar DEPOIS de criar OAuth no Google Cloud.
4. Authentication → URL Configuration → Redirect URLs: adicione io.seuapp.app://login-callback/.
5. Para dados de usuários/famílias, habilite Row Level Security (RLS) e escreva políticas antes de liberar acesso. Auth sozinho não protege tabelas.
6. Guarde scripts SQL versionados em 01_data/migrations/. NÃO coloque senha de banco ou service_role no Flutter.

## 9 — Google Cloud OAuth
1. console.cloud.google.com → criar/selecionar projeto.
2. Google Auth Platform → Branding: nome do aplicativo, email de suporte e demais campos.
3. Audience: External se apropriado; em Testing adicione emails em Test users. Publicação/verificação podem exigir passos extras.
4. Clients → Create Client → Web application; nome: Meu App Supabase.
5. Authorized redirect URIs: https://SEU_PROJECT_REF.supabase.co/auth/v1/callback (exato).
6. Copie Client ID e Client Secret para Supabase → Authentication → Providers → Google, habilite e salve.
7. Nunca coloque Client Secret no repositório ou Flutter.
8. O app precisa somente de openid, email e profile para login básico; não precisa de Photos, Drive ou vídeos.
9. Branding mostra o nome do app, mas o Google também pode mostrar o domínio técnico do Supabase na tela de consentimento.

## 10 — Flutter + Supabase
No terminal:

    cd 03_front
    flutter pub add supabase_flutter
    flutter pub get

Substitua main.dart:

    import 'package:flutter/material.dart';
    import 'package:supabase_flutter/supabase_flutter.dart';
    import 'app.dart';
    Future<void> main() async {
      WidgetsFlutterBinding.ensureInitialized();
      await Supabase.initialize(
        url: 'https://SEU_PROJECT_REF.supabase.co',
        publishableKey: 'SUA_CHAVE_PUBLICAVEL',
      );
      runApp(const MyApp());
    }

Troque placeholders por dados do SEU projeto. Publishable key é pública; service_role é secreta.

## 11 — Deep link Android e iOS
Use SEMPRE o mesmo redirectTo: io.seuapp.app://login-callback/ no Flutter e Supabase.

Android: 03_front/android/app/src/main/AndroidManifest.xml. Na tag manifest, confirme a permissão:
    <uses-permission android:name="android.permission.INTERNET" />
Dentro da activity principal, preserve os filtros existentes e adicione:
    <intent-filter>
      <action android:name="android.intent.action.VIEW" />
      <category android:name="android.intent.category.DEFAULT" />
      <category android:name="android.intent.category.BROWSABLE" />
      <data android:scheme="io.seuapp.app" android:host="login-callback" />
    </intent-filter>

iOS: 03_front/ios/Runner/Info.plist. Dentro do dict principal:
    <key>CFBundleURLTypes</key>
    <array><dict><key>CFBundleURLSchemes</key><array>
      <string>io.seuapp.app</string>
    </array></dict></array>

Este scheme é EXEMPLO: escolha um único por app. Para produção, considere App Links/Universal Links e domínio verificado. Mudanças nativas exigem parar e recompilar; hot reload não basta.

## 12 — Login Google REAL
Na LoginPage, use StatefulWidget com bool _loading, assinatura de auth.onAuthStateChange e cancelamento da assinatura em dispose. No clique do botão:

    await Supabase.instance.client.auth.signInWithOAuth(
      OAuthProvider.google,
      redirectTo: 'io.seuapp.app://login-callback/',
      authScreenLaunchMode: LaunchMode.externalApplication,
    );

Ao receber AuthState com session != null, com widget mounted, navegue usando Navigator.pushNamedAndRemoveUntil(context, '/home', (_) => false). Capture AuthException e mostre SnackBar. Desabilite o botão durante loading. Não navegue para Home somente por ter clicado: aguarde sessão REAL.

Na Splash, depois de inicializar Supabase:
    final loggedIn = Supabase.instance.client.auth.currentSession != null;
    Navigator.of(context).pushReplacementNamed(loggedIn ? '/home' : '/login');

Na rota Home, verifique currentSession != null; se não existir, mostre Login. Isso é apenas proteção visual; dados no banco precisam de RLS.

No botão Sair:
    await Supabase.instance.client.auth.signOut(scope: SignOutScope.local);
    if (context.mounted) {
      Navigator.of(context).pushNamedAndRemoveUntil('/login', (_) => false);
    }

SignOutScope.local desconecta somente o aparelho atual. O signOut() sem escopo pode encerrar sessões de outros dispositivos. Apple Login requer configuração própria no Apple Developer/Supabase; não considerar concluído por existir botão.

## 13 — Testes obrigatórios
- Rodar flutter analyze e flutter run dentro de 03_front.
- Splash → Login → Google → retorno ao app → Home.
- Verificar usuário em Supabase → Authentication → Users.
- Fechar/reabrir sem logout: deve ir para Home.
- Logout: deve ir para Login; novo login pode entrar direto porque Google já autorizou.
- Repetir em outro aparelho; a mesma conta pode manter sessões independentes.
- Para rever consentimento, revogar em myaccount.google.com/connections; não precisa excluir usuário Supabase.
- Em emulador novo, termos Google, backup de fotos/vídeos e sincronização Chrome são configurações da conta Android/Google, não necessariamente permissões do aplicativo.
- Idioma da página Google: requisito futuro é acompanhar idioma do CELULAR; verificar suporte do provedor, pois app não controla toda a interface Google.

## 14 — Problemas comuns
- "Expected to find project root": cd 03_front.
- "MissingPluginException ... shared_preferences": parar debug completamente, flutter clean, flutter pub get, compilar novamente.
- "No suitable Android AVD system images": Android Studio Device Manager → baixar imagem com Google Play (ex.: Android 15 API 35).
- "redirect_uri_mismatch": conferir callback HTTPS do Supabase no Google Cloud.
- Login não retorna ao app: conferir redirectTo, Redirect URLs, manifest e Info.plist; rebuild completo.
- "This account already exists on your device": Google já está cadastrado no emulador; selecionar conta existente ou gerenciar contas do Android.
- OAuth pede fotos/vídeos: diferenciar setup Android/Google dos escopos de autorização do app.
- Mudança de arquivos nativos sem efeito: parar F5, flutter clean, flutter pub get, F5 novamente.

## 15 — Sincronização diária
Na raiz: git status → git pull → ler código atual → alterar → flutter analyze/testar → git add . → git commit -m "mensagem" → git push. Nunca usar reset --hard sem saber o que será perdido.

## 16 — Estado de referência do Butler
Em outubro/2026, Butler tem login Google real Supabase funcionando em Pixel 8 Pro e Pixel 9, Splash, Login, Home e sessão persistente. Apple Login ainda não configurado. O nome do arquivo responsivo é PROVISÓRIO; kolors e responsive deste manual são PADRÕES PARA NOVOS APPS, não afirmação de que já existam no Butler. Não reutilizar URL/chaves do Supabase Butler em novos apps.

CHECKLIST: [ ] Git e Flutter instalados; [ ] pasta local; [ ] GitHub conectado; [ ] 4 pastas; [ ] Flutter criado; [ ] arquivos main/app/routes/kolors/responsive; [ ] Splash/Login/Home; [ ] commit; [ ] Supabase; [ ] Google Cloud OAuth; [ ] deep link; [ ] login real; [ ] sessão persistente; [ ] RLS; [ ] testes; [ ] push.

REGRA FINAL: ESTRUTURA → APP MÍNIMO → AUTENTICAÇÃO → TESTE → EVOLUÇÃO.
