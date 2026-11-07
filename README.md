# DJANGO Admin

Painel administrativo React + TypeScript + Vite + Supabase para o projecto `qfdjiqacjeafquoscbnj`.

## Requisitos
- Node.js 20.19+ ou 22.12+
- Uma chave Supabase **publishable** (preferível) ou anon legada.
- Conta Supabase Auth que esteja registada como administrador activo em `public.motaja_admins`.

## Instalação (Ubuntu)
```bash
unzip DJANGO_Admin_Source.zip
cd DJANGO_Admin
cp .env.example .env
nano .env
npm install
npm run dev
```
Abrir `http://localhost:5173`.

## Configuração
No `.env`:
```env
VITE_SUPABASE_URL=https://qfdjiqacjeafquoscbnj.supabase.co
VITE_SUPABASE_ANON_KEY=sua_chave_publishable_ou_anon
```
A chave pode ser obtida no Supabase Dashboard > Project Settings > API Keys. **Nunca colocar `service_role` ou secret key no frontend.**

## Segurança / acesso
1. O login é feito por Supabase Auth.
2. Após login, o painel consulta `motaja_admins` e exige `active = true` para o `auth.uid()`.
3. Se não houver administrador activo, o acesso é negado por defeito. O contexto actual do projecto indicava zero administradores activos; será necessário provisionar o primeiro administrador através de um processo seguro no backend/Supabase Dashboard.
4. As tabelas devem ter RLS e políticas restritas a administradores. O bloqueio visual do frontend não substitui RLS.
5. Não há operações destrutivas nem aprovação de documentos nesta primeira versão.

## Módulos
- Visão geral: métricas calculadas a partir dos últimos 100 registos consultados.
- Viagens: `motaja_rides`.
- Motoristas: `motaja_drivers`.
- Passageiros: `motaja_profiles`.
- Acessibilidade: `motaja_accessibility_support_cases` (sem expor notas/documentos médicos).
- Pagamentos: `motaja_payments` (consulta).
- Notificações: `motaja_notification_inbox`.
- Agentes IA: `motaja_agent_sessions`.
- Entregas: reservado; esquema não confirmado na inspecção.
- Administradores e configurações: protegidos em modo de consulta até endpoints administrativos auditados.

## Build
```bash
npm run build
npm run preview
```

## Limitações desta entrega
- O painel está ligado às tabelas identificadas, mas o acesso real depende das políticas RLS existentes.
- Não foi criado nenhum administrador, alterado schema ou publicado o website.
- O módulo de entregas e operações de escrita precisam de confirmar as tabelas/endpoints e respectivas regras de autorização.
