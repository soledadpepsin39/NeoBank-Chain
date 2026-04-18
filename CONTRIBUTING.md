# 🤝 Contributing to NeoBank Chain

> *"The future of finance is built by the community, for the community."*
> — Ghost | Founder, NeoBank Chain

---

## 👋 Welcome, Contributor!

Thank you for your interest in NeoBank Chain — the world's first true bridge between Centralized Finance, Decentralized Finance, Islamic Finance, and AI-powered banking.

Whether you are a **Solana developer**, **mobile engineer**, **UI/UX designer**, **Islamic finance expert**, **compliance professional**, or simply a **believer in financial freedom for everyone** — there is a place for you here.

We build in public. We build together. We build for everyone.

---

## 🌍 Our Values

Before contributing, please understand what drives this project:

- **Inclusion first** — we build for the 1.7 billion unbanked, not just for crypto-native users
- **Ethical finance** — we respect Islamic finance principles as a core pillar, not an afterthought
- **Security above all** — we handle real money; every line of code matters
- **Transparency** — all decisions, architectures, and trade-offs are documented publicly
- **Quality** — we prefer doing fewer things exceptionally well over many things poorly

---

## 🚀 How to Contribute

### Step 1 — Understand the project
Read the following before contributing:
- `README.md` — product overview
- `VISION.md` — mission and values
- `WHITEPAPER.md` — technical and economic details
- `ROADMAP.md` — current priorities

### Step 2 — Set up your environment

```bash
# Fork the repository on GitHub
# Clone your fork
git clone https://github.com/YOUR_USERNAME/NeoBank-Chain.git
cd NeoBank-Chain

# Create a feature branch
git checkout -b feature/your-feature-name
# or
git checkout -b fix/bug-description
# or
git checkout -b docs/documentation-improvement
```

### Step 3 — Make your changes
Write your code, documentation, or design files.

### Step 4 — Commit with a clear message

```bash
# Use conventional commits format
git commit -m "feat: add Islamic finance Mourabaha calculator"
git commit -m "fix: correct USDC balance display on dashboard"
git commit -m "docs: add Arabic translation to README"
git commit -m "security: fix reentrancy vulnerability in withdrawal"
```

**Commit prefixes:**
- `feat:` — new feature
- `fix:` — bug fix
- `docs:` — documentation only
- `security:` — security improvement
- `test:` — adding or updating tests
- `refactor:` — code restructuring without behavior change
- `design:` — UI/UX changes
- `i18n:` — internationalization / translations

### Step 5 — Push and open a Pull Request

```bash
git push origin feature/your-feature-name
```

Then open a Pull Request on GitHub with:
- Clear title describing what you changed
- Description of why you made this change
- Screenshots for UI changes
- Test results for code changes

---

## 🏗️ Areas Where We Need Help

### 🔥 High Priority Now (Phase 1)

**Documentation & Translation**
- Arabic translation of all documentation
- French translation of all documentation
- Indonesian translation of all documentation
- Technical documentation for smart contracts

**Design**
- Figma wireframes for all screens
- Brand identity refinement
- App icon design
- Marketing materials

**Community**
- Discord community management
- Social media content (Twitter/X)
- Islamic finance community outreach
- DeFi community outreach

### 💻 Development (Phase 2+)

**Blockchain (Rust/Solana)**
- Wallet program development
- Transfer program development
- Islamic finance smart contracts (Mourabaha)
- B2B Credoc program

**Mobile (React Native)**
- Onboarding & KYC screens
- Dashboard & wallet view
- Transfer screens (CeFi + DeFi routing)
- Claude AI chat interface
- Islamic finance products UI
- B2B professional suite UI

**Backend (Node.js)**
- REST API development
- GraphQL schema design
- KYC/AML integration (Jumio)
- DeFi protocol integrations (Jupiter, Jito, Kamino)
- Apple Pay / Google Pay integration

**Security**
- Smart contract security review
- Penetration testing
- Security documentation

### ⚖️ Islamic Finance Expertise
- Shariah compliance review of product designs
- Mourabaha contract structuring
- Zakat calculation methodology
- Connection to Shariah scholars for certification

### 📋 Compliance & Legal
- MiCA (EU) compliance documentation
- UAE ADGM licensing research
- KYC/AML best practices
- FATF Travel Rule implementation

---

## 📐 Code Standards

### TypeScript
```typescript
// ✅ Always use strict TypeScript
// ✅ Always handle errors explicitly
// ✅ Always validate inputs
// ✅ Use enums for constants
// ✅ Write tests for every function (target: >90% coverage)
```

### Rust (Smart Contracts)
```rust
// ✅ Check-Effects-Interactions pattern on every instruction
// ✅ Owner verification on every sensitive operation
// ✅ Use PDAs (Program Derived Addresses) for deterministic accounts
// ✅ Emit events for all state changes
// ✅ Document every public function with /// comments
```

### Security Rules (Non-negotiable)
- Never store private keys or secrets in code
- Never skip input validation
- Always use parameterized queries (no SQL injection)
- Always verify ownership before state changes
- Always test edge cases and failure modes

---

## 🔒 Security Vulnerabilities

**If you discover a security vulnerability:**

DO NOT open a public GitHub issue.

Instead, email: **neobankchain@gmail.com** with subject: `[SECURITY] Brief description`

Include:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Your suggested fix (if any)

We will respond within 48 hours and credit you in our security acknowledgments.

A bug bounty program will be launched in Phase 4.

---

## 🌐 Internationalization

NeoBank Chain targets a global audience. We especially need:

- **Arabic** — primary language for MENA Islamic finance users
- **French** — Morocco, Tunisia, Algeria, West Africa, France
- **Indonesian** — world's largest Muslim population
- **Urdu** — Pakistan, Indian subcontinent
- **Hausa** — West Africa

Translation files will be organized in `i18n/[language-code]/`.

---

## ✅ Pull Request Checklist

Before submitting, verify:

- [ ] I have read `CONTRIBUTING.md`
- [ ] My code follows the project's code standards
- [ ] I have written tests for new functionality
- [ ] All existing tests pass
- [ ] I have updated documentation if needed
- [ ] My commit messages follow the conventional commits format
- [ ] I have not introduced any security vulnerabilities
- [ ] UI changes include screenshots
- [ ] Smart contract changes have been reviewed for security

---

## 📬 Get in Touch

- **Email:** neobankchain@gmail.com
- **GitHub Issues:** For bugs and feature requests
- **GitHub Discussions:** For questions and ideas
- **Discord:** Coming soon

---

## 🏆 Recognition

All contributors are recognized:
- Listed in `CONTRIBUTORS.md`
- Mentioned in release notes
- Early access to beta when launched
- Priority consideration for team positions as we grow

---

<div align="center">

**NeoBank Chain** — *Your bank. Your rules. On blockchain.* 🚀

*We build for the 1.7 billion. Together.*

*CONTRIBUTING.md v2.0 — April 2026*

</div>
