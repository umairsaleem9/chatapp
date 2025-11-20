# GitHub Context Sample Data

Use these lightweight files in any sandbox repository to validate the GitHub context + AI routing flow. The goal is to give the assistant deterministic file paths and branch names it can cite when you run prompts like “Generate a story for X based on our repo.”

## Repository Layout

```
sample-repo/
├─ apps/web/src/features/onboarding/OnboardingWizard.tsx
├─ apps/web/src/features/onboarding/__tests__/OnboardingWizard.test.tsx
├─ packages/api/src/routes/stories/createStory.ts
├─ packages/api/src/routes/stories/__tests__/createStory.test.ts
├─ docs/product/onboarding-story.md
└─ docs/architecture/github-context.md
```

### apps/web/src/features/onboarding/OnboardingWizard.tsx
```tsx
export const OnboardingWizard = () => {
  return (
    <section data-testid="onboarding-wizard">
      <h1>Onboarding Wizard</h1>
      <p>Guides new users through repo-backed story setup.</p>
    </section>
  )
}
```

### packages/api/src/routes/stories/createStory.ts
```ts
export const createStory = async (payload: { title: string }) => {
  return {
    id: "story-sample",
    title: payload.title,
    source: "github-context",
    repoPath: "apps/web/src/features/onboarding/OnboardingWizard.tsx"
  }
}
```

### docs/product/onboarding-story.md
```
# Story: Guided Onboarding

- Pull UI snippets from `apps/web/src/features/onboarding/OnboardingWizard.tsx`
- Reference API logic in `packages/api/src/routes/stories/createStory.ts`
```

## Testing Checklist

1. Create a scratch repo (or folder) with the structure above and commit it on a branch named `feature/github-context-demo`.
2. Connect that repo + branch via Workspace → Configure GitHub Repositories.
3. Trigger chat with “Generate a story for Guided Onboarding based on our repo.”
4. Expect the response to mention the `OnboardingWizard.tsx` UI and `createStory.ts` API path.

Feel free to duplicate the layout with different filenames/branches to cover other scenarios. The assistant only needs consistent, real paths to surface in its answer. 

