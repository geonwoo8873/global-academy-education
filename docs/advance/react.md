# 1. React Installation

### Node.js install version check cli
```bash
node --version
-> 24.1.0
```

### Npm package lib of install version check cli

```bash
npm -v
-> 12.1.0
```

> [!NOTE]
> * **npm의 버전이 `11.*.*` 일경우 Terminal에서 Major 버전이 릴리즈 했다는 문구가 나오는데, 이는 사용자의 선택에 따라 버전을 유지할 것인지 아니면 업데이트를 할 것인지 정하면된다.**
> * **작성 기점으로 PS에서는 npm cmd가 받아들이지 못하여 bash를 통해 확인을 했으며, Windows 11 체제 변환과 유저 정책으로 인해 차단 되었거나 일시적인 `Blocking` 현상으로 파악된다.**

### React installation cli

```bash
npm <option> <lib name>@<version> <directory name> -- --<option> <framework name>
```

```bash
npm create vite@latest <directory_name> -- --template react
```

### Lint select

* ESLint [표준]

* Oxlint [확장]

### React [Vite] installing package

```bash
Need to install the following packages:
create-vite@9.2.1
Ok to proceed? (y) y
npm notice run npx
npm notice run create-vite react-web-lab --template react
│
◇  Which linter to use?
│  ESLint
│
◇  Install with npm and start now?
│  Yes
│
◇  Scaffolding project in C:\Users\geonw\OneDrive\GitHub Repositorys\Global-Academy\react-web-lab...
│
◇  Installing dependencies with npm...

added 143 packages, and audited 144 packages in 8s

31 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
│
◇  Starting dev server...
npm notice run react-web-lab@0.0.0 dev
npm notice run vite

  VITE v8.3.1  ready in 2220 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
```

---

* Props

* useState