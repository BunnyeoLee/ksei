# 경성전자고등학교 총동창회 홈페이지

이 폴더를 깃허브에 올리면 누구나 접속할 수 있는 홈페이지가 됩니다.
회원가입·로그인·게시판·사진 올리기는 무료 서비스 **Supabase**에 연결해야 작동합니다.
아래 순서대로 한 번만 설정하면 됩니다(약 30분).

| 파일 | 역할 |
|---|---|
| `index.html` | 홈페이지 전체(디자인, 소개 페이지, 게시판) |
| `config.js` | Supabase 연결 정보를 넣는 곳 |
| `supabase-setup.sql` | 회원·게시판·사진 저장소와 보안 규칙, 이전 공지사항 30건 |
| `images/` | 사진을 넣는 폴더(아래 5단계) |

---

## 1단계. Supabase 프로젝트 만들기

1. https://supabase.com 에 접속해 **Start your project**를 누르고 깃허브 계정으로 가입합니다.
2. **New project**를 누르고 이름은 `ksei`, Region은 **Northeast Asia (Seoul)**을 고릅니다.
   Database Password는 자동 생성된 값을 그대로 쓰고 따로 적어 둡니다. **Create new project**를 누르고 1~2분 기다립니다.

## 2단계. 데이터베이스 설정

1. 왼쪽 메뉴의 **SQL Editor**를 엽니다.
2. `supabase-setup.sql` 파일을 메모장으로 열어 전체를 복사해 붙여 넣고 **Run**을 누릅니다.
   "Success" 가 나오면 됩니다. (회원·게시판·사진 저장소가 만들어지고 이전 공지사항 30건이 들어갑니다.)
3. 왼쪽 메뉴 **Authentication** → **Sign In / Providers**(또는 Providers → Email)에서
   **Confirm email**을 끕니다. 끄지 않으면 가입할 때마다 인증 메일을 눌러야 합니다.

## 3단계. 연결 정보를 config.js에 넣기

1. 왼쪽 아래 톱니바퀴 **Project Settings** → **API**(또는 Data API)를 엽니다.
2. **Project URL**과 **anon public** 키를 복사해 `config.js`의 따옴표 안에 붙여 넣습니다.

```js
window.KSEI_CONFIG = {
  supabaseUrl: "https://abcdxyz.supabase.co",
  supabaseAnonKey: "eyJhbGciOi..."
};
```

> anon public 키는 공개되어도 안전합니다(보안 규칙이 데이터를 지킵니다).
> **service_role** 키는 절대 넣지 마세요.

## 4단계. 깃허브에 올리기

1. https://github.com 에서 오른쪽 위 **+** → **New repository**.
   이름 `ksei`, **Public** 선택 → **Create repository**.
2. 새 저장소 화면의 **uploading an existing file** 링크(또는 Add file → Upload files)를 누르고,
   이 폴더 안의 파일과 `images` 폴더를 **모두 끌어다 놓은 뒤** **Commit changes**.
3. 저장소의 **Settings** → 왼쪽 **Pages** → Source는 **Deploy from a branch**, Branch는 **main / (root)** → **Save**.
4. 1~2분 뒤 같은 화면 위쪽에 주소가 나옵니다: `https://깃허브아이디.github.io/ksei/`
5. Supabase로 돌아가 **Authentication → URL Configuration → Site URL**에 이 주소를 넣고 저장합니다.

## 5단계. 관리자 계정 만들기

1. 홈페이지에서 **회원가입**을 누르고 다음과 같이 가입합니다.
   - 이름: 총동창회 관리자 / 아이디: `admin2026` / 비밀번호: `admin2222`
   - 이메일: 사무국 이메일 / 전화번호: 사무국 번호
2. Supabase **SQL Editor**에서 아래 한 줄을 실행하면 관리자가 됩니다.

```sql
update public.profiles set role = 'admin' where username = 'admin2026';
```

관리자는 모든 게시판(공지사항 포함)에 글을 쓰고, 누구의 글·댓글이든 수정·삭제할 수 있습니다.
화면 위쪽 **관리자** 메뉴에서 회원 목록을 보고 권한(회원/관리자/이용 정지)을 바꿀 수 있습니다.

> 보안을 위해 운영을 시작하면 **내 정보**에서 관리자 비밀번호를 더 길고 복잡하게 바꾸세요.

## 6단계. 사진 넣기 (images 폴더)

파일 이름만 맞춰 `images` 폴더에 넣으면 자동으로 화면에 나타납니다. 없으면 깔끔한 기본 디자인으로 보입니다.

| 파일 이름 | 들어가는 곳 | 이전 홈페이지 원본 |
|---|---|---|
| `images/hero.jpg` | 첫 화면 큰 사진 | `/img/main_bn01.png` (2024 정기총회) |
| `images/logo.png` | 왼쪽 위 휘장 | 사무국에 고화질 휘장 요청 권장 |
| `images/map.jpg` | 오시는 길 약도 | `/img/01_sub/map.jpg` |
| `images/presidents/mas01.jpg` ~ `mas14.jpg` | 역대 회장 사진 (mas08은 회장 인사말 사진으로도 쓰임) | `/img/01_sub/mas01.jpg` ~ `mas14.jpg` |
| `images/greeting-president.png` | 회장 인사말 원본 보기 | `/img/01_sub/sub01.png` |
| `images/greeting-principal.png` | 학교장 인사말 원본 보기 | `/img/01_sub/sub07.png` |
| `images/org-2019.jpg` | 조직도 원본 보기 | `/img/01_sub/about.jpg` |
| `images/principal.jpg` | 학교장 사진 | 학교에 요청 |

깃허브 저장소에서 **Add file → Upload files**로 `images` 폴더째 끌어다 놓으면 됩니다.
포토갤러리 사진은 로그인 후 홈페이지의 **사진 올리기**로 올립니다.

## 내용 고치기

- 소개 페이지(인사말, 임원, 연혁 등)는 `index.html` 안에 있습니다. 깃허브에서 파일을 열고 연필 아이콘으로 고친 뒤 Commit 하면 1~2분 뒤 반영됩니다.
- 공지사항·게시판 글은 홈페이지에서 관리자로 로그인해 바로 쓰고 고칩니다.

## 나중에 ksei.co.kr 주소 연결 (선택)

깃허브 **Settings → Pages → Custom domain**에 `www.ksei.co.kr`을 넣고,
도메인 업체 관리 화면에서 `www` CNAME을 `깃허브아이디.github.io`로 바꾸면 기존 주소로 새 홈페이지가 열립니다.
