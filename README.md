# 🌐 Remote Module (User Panel)

This remote module exposes a `UserPanel` component via Webpack Module Federation.

---

## 📁 Project Structure

```
remote-module/
├── src/
│   ├── App.tsx         # Component exposed to the host
│   └── index.tsx       # Entry point (for standalone mode)
├── public/             # Static assets
├── package.json
├── webpack.config.js
└── tsconfig.json
```

## ⚙️ How It Works

The remote module is a self-contained application that exposes a single component (`Dashboard`) via Module Federation.

### 🧩 Exposing Components

1. **Webpack Configuration**:

```js
new ModuleFederationPlugin({
  name: "remote",
  filename: "remoteEntry.js",
  exposes: {
    "./Dashboard": "./app/App",
  },
  shared: {
    react: { singleton: true, eager: true },
    "react-dom": { singleton: true, eager: true },
  },
})
```

2. **Entry Point**:

```tsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
const root = ReactDOM.createRoot(document.getElementById('root')!);
root.render(<App />);
```

3. **Component Implementation**:

```tsx
import React from 'react';
import { Button } from './ui/button';

export default function UserPanel() {
  return (
    <div>
      <h2>User Panel</h2>
      <Button>Click Me</Button>
    </div>
  );
}
```

## 🚀 Getting Started

### Prerequisites

- Node.js (v18 or higher)
- Yarn

### Installation

```bash
git clone
cd mf-remote-app
yarn install
```

### Running the Application

```bash
yarn start
```

Runs at [http://localhost:3001](http://localhost:3001).

## 🏗 Production Build

```bash
yarn build
```

Artifacts will be stored in the `dist/` directory.

## 📝 Notes

- Host must be configured to load remote from `http://localhost:3001/remoteEntry.js`
- Production should use a deployed URL for the remote.
