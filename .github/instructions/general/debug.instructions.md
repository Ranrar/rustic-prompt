Your primary objective is to systematically identify, analyze, and resolve bugs in the application. This workflow leverages best practices for structured debugging.

## Phase 1: Problem Assessment

### 1. Gather Context
- **Error Messages**: Capture any error messages or stack traces.
- **Codebase Structure**: Review recent changes and dependencies.
- **Expected vs. Actual Behavior**: Clearly define the expected outcome and compare with the actual result.
- **Test Failures**: Identify failing tests and their contexts.  

### 2. Reproduce the Bug
- **Steps to Reproduce**: Document exact steps.
- **Logs and Outputs**: Collect relevant logs and outputs.
- **Bug Report**: Include:
  - Steps to reproduce
  - Expected behavior
  - Actual behavior
  - Error messages / stack traces
  - Environment details

## Phase 2: Investigation

### 3. Root Cause Analysis
- **Code Execution Path**: Trace the execution path.
- **Variable States**: Examine variable values at critical points.
- **Data Flows**: Understand how data flows through the system.
- **Common Issues**: Check for null references, off-by-one errors, race conditions, and incorrect assumptions.
- **Component Interactions**: Analyze dependencies and interactions.
- **Git History**: Review recent changes for potential regressions.  

### 4. Hypothesis Formation
- **Form Hypotheses**: Specific guesses about root cause.
- **Prioritize**: Based on likelihood and impact.
- **Verification Plan**: Steps to test each hypothesis.

## Phase 3: Resolution

### 5. Implement Fix
- **Targeted Changes**: Minimal edits addressing root cause.
- **Code Consistency**: Align with existing code patterns.
- **Defensive Programming**: Add checks to prevent recurrence.
- **Edge Cases**: Consider unusual or extreme inputs.  


### 6. Verification
- **Test Execution**: Run tests to confirm fix.
- **Reproduce Steps**: Re-do reproduction steps to verify resolution.
- **Regression Testing**: Ensure no new issues introduced.
- **Edge Case Testing**: Validate edge cases.  

## Phase 4: Quality Assurance

### 7. Code Quality
- **Review**: Ensure readability, maintainability, and performance.
- **Testing**: Add/update tests for the fixed issue.
- **Documentation**: Update documentation as needed.
- **Similar Issues**: Check for similar bugs in other areas.

### 8. Final Report
- **Summary**: Concise description of issue and fix.
- **Root Cause**: Explain underlying problem.
- **Preventive Measures**: Document actions to avoid recurrence.
- **Recommendations**: Suggest improvements.  