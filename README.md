# Component Structure and Responsibilities

This document outlines a high-level component structure for two sign-up forms:

- **Form #1:** Requires username and password  
- **Form #2:** Requires username, password, and gender

Both forms submit to different API endpoints.

## Validation & State Management

**`react-hook-form`**:  
- Used within each form component (e.g., `SignUpFormBasic`, `SignUpFormWithGender`).
- Handles form state, registration of fields, and submission.

**`zod`**:  
- Defines schemas for form validation.
- Integrated with `react-hook-form` via `zodResolver` to ensure all form data adheres to the defined schema.


## Components

1. **`SignUpFormBasic`** (root component for the **Form #1**)
2. **`SignUpFormWithGender`** (root component for the **Form #2**)
3. **`PasswordField`** (reusable, specialized text field)
4. **`GenderSelectField`** (reusable, specialized select field)
5. **`TextField`** (reusable)
6. **`SelectField`** (reusable)
7. **`Button`** (reusable)

## Component Tree Structure

### Form #1 (Username & Password)
```sh
SignUpFormBasic
   ├─ TextField (username)
   ├─ PasswordField (password)
   └─ Button (submit)
```

### Form #2 (Username, Password & Gender)

```sh
SignUpFormWithGender
   ├─ TextField (username)
   ├─ PasswordField (password)
   ├─ GenderSelectField (gender)
   └─ Button (submit)
```


## Responsibilities


### `SignUpFormBasic`
**Role:**  
A specialized form for gathering a username and password.

**Details:**
- Integrates `react-hook-form` using `useForm()` and `zodResolver` with a `zod` schema for validation.
- Uses `TextField`component for username, `PasswordField` for password and `Button` to submit.
- On submit, uses the validated data to call the corresponding API endpoint (e.g. `/api/signup`).

### `SignUpFormWithGender`
**Role:**  
A specialized form for gathering username, password, and gender.

**Details:**
- Uses `react-hook-form` and `zodResolver` with a different `zod` schema that includes gender.
- Renders `TextField` for username, `PasswordField` for password, `GenderSelectField` for gender, and a `Button` to submit.
- On submit, validates against the schema and then sends the data to `/api/signup_gender`


### `TextField` (Re-usable)
**Role:**  
A text input with a label, validation messages, and related UI.

**Details:**
- Accepts `name`, `label`, `type`, `value`, `onChange`, etc (extends `InputHTMLAttributes<HTMLInputElement>`)
- Displays validation states and error messages.

### `PasswordField` (Re-usable)
**Role:**  
A specialized text input for passwords.

**Details:**
- Inherits `TextField` behavior but optimized for password input.
- May include a show/hide password toggle.
- Shows a list of password requirements below the input (e.g., "8+ characters", "At least one uppercase letter"):
  - Each requirement highlighted green if met.
  - Each requirement highlighted red if not met and if there was an attempt to submit the form (late validation)
- Handles password-specific validation or requirements.

### `SelectField` (Re-usable)
**Role:**  
A generic dropdown for choosing from multiple options.

**Details:**
- Accepts `name`, `label`, `options`, `value`, `onChange`.
- Displays validation messages as needed.

### `GenderSelectField` (Re-usable)
**Role:**  
A `SelectField` pre-configured for gender selection.

**Details:**
- Provides predefined gender options.
- Inherits `SelectField` behavior (props, validation, etc.).

### `Button` (Re-usable)
**Role:**  
A general-purpose button.

**Details:**
- Triggers form submissions or other actions.
- Can show loading or disabled states.

