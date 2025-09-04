# Main Branch Protection

This repository implements a dual-layer protection mechanism to prevent direct pushes to the `main` branch.

## Protection Layers

### 1. Client-side Protection (Husky Pre-push Hook)

A Git pre-push hook prevents developers from pushing directly to the main branch from their local machines.

**Location**: `.husky/pre-push`

**How it works**: 
- Checks the current branch name before any push operation
- If the current branch is `main`, the push is blocked with an informative error message
- Provides clear instructions on the proper workflow

### 2. Server-side Protection (GitHub Actions)

A GitHub Actions workflow that runs on any push to the main branch and immediately fails.

**Location**: `.github/workflows/protect-main.yml`

**How it works**:
- Triggers on push events to the `main` branch
- Immediately fails with an error message
- Prevents the push from completing

## Proper Workflow

To contribute to this project:

1. **Create a feature branch**:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes and commit**:
   ```bash
   git add .
   git commit -m "Your commit message"
   ```

3. **Push your feature branch**:
   ```bash
   git push origin feature/your-feature-name
   ```

4. **Create a Pull Request** on GitHub to merge your changes into `main`

## Error Messages

If you attempt to push to main, you'll see one of these messages:

### Client-side (pre-push hook):
```
❌ ERROR: Direct pushes to the 'main' branch are not allowed!

Please use the following workflow instead:
1. Create a feature branch: git checkout -b feature/your-feature-name
2. Make your changes and commit them
3. Push your feature branch: git push origin feature/your-feature-name
4. Create a pull request to merge into main
```

### Server-side (GitHub Actions):
```
❌ Direct pushes to the main branch are not allowed!
Please create a feature branch and submit a pull request instead.
Use: git checkout -b feature/your-feature-name
```

## Bypassing Protection (For Repository Administrators)

If you need to bypass this protection in exceptional circumstances:

1. **Temporarily disable the pre-push hook**:
   ```bash
   git push --no-verify origin main
   ```

2. **Or push via GitHub UI** with appropriate permissions

⚠️ **Warning**: Bypassing protection should only be done by repository administrators and in exceptional circumstances.