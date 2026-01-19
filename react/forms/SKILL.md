---
name: forms
description: >
  Forms in React.
  Trigger: When working with forms - controlled inputs, validation, React Hook Form, Zod
license: Apache-2.0
metadata:
  author: ai-agent-skills
  version: "1.0"
  scope: [ui]
  auto_invoke: "React Forms / Validation"
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# React Forms

## Controlled Components

```typescript
import { useState } from 'react'

function LoginForm() {
  const [form, setForm] = useState({ email: '', password: '' })
  
  const handleSubmit = (e: FormEvent) => {
    e.preventDefault()
    console.log(form)
  }
  
  const handleChange = (e: ChangeEvent<HTMLInputElement>) => {
    setForm(prev => ({
      ...prev,
      [e.target.name]: e.target.value
    }))
  }
  
  return (
    <form onSubmit={handleSubmit}>
      <input
        name="email"
        value={form.email}
        onChange={handleChange}
        type="email"
      />
      <input
        name="password"
        value={form.password}
        onChange={handleChange}
        type="password"
      />
      <button type="submit">Login</button>
    </form>
  )
}
```

## useForm Hook (React Hook Form)

```typescript
import { useForm } from 'react-hook-form'

interface FormData {
  name: string
  email: string
  age: number
}

function RegistrationForm() {
  const {
    register,
    handleSubmit,
    formState: { errors }
  } = useForm<FormData>()
  
  const onSubmit = (data: FormData) => {
    console.log(data)
  }
  
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input
        {...register('name', { required: 'Name is required' })}
      />
      {errors.name && <span>{errors.name.message}</span>}
      
      <input
        {...register('email', {
          required: 'Email is required',
          pattern: {
            value: /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i,
            message: 'Invalid email'
          }
        })}
      />
      {errors.email && <span>{errors.email.message}</span>}
      
      <input
        type="number"
        {...register('age', {
          required: true,
          min: { value: 18, message: 'Must be 18+' }
        })}
      />
      
      <button type="submit">Submit</button>
    </form>
  )
}
```

## Zod + React Hook Form

```typescript
import { z } from 'zod'
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'

const schema = z.object({
  name: z.string().min(2, 'Name must be 2+ chars'),
  email: z.string().email('Invalid email'),
  age: z.number().min(18, 'Must be 18+')
})

type FormData = z.infer<typeof schema>

function Form() {
  const { register, handleSubmit, formState: { errors } } =
    useForm<FormData>({
      resolver: zodResolver(schema)
    })
  
  return (
    <form onSubmit={handleSubmit(d => console.log(d))}>
      <input {...register('name')} />
      {errors.name && <span>{errors.name.message}</span>}
      
      <input {...register('email')} />
      {errors.email && <span>{errors.email.message}</span>}
      
      <input type="number" {...register('age', { valueAsNumber: true })} />
      {errors.age && <span>{errors.age.message}</span>}
      
      <button type="submit">Submit</button>
    </form>
  )
}
```

## Select and Textarea

```typescript
const [selected, setSelected] = useState('')

<select value={selected} onChange={e => setSelected(e.target.value)}>
  <option value="">Select...</option>
  <option value="a">Option A</option>
  <option value="b">Option B</option>
</select>

<textarea
  value={text}
  onChange={e => setText(e.target.value)}
  rows={4}
/>
```

## Checkbox and Radio

```typescript
const [agree, setAgree] = useState(false)

<input
  type="checkbox"
  checked={agree}
  onChange={e => setAgree(e.target.checked)}
/>

const [color, setColor] = useState('blue')

<input
  type="radio"
  name="color"
  value="blue"
  checked={color === 'blue'}
  onChange={e => setColor(e.target.value)}
/>
```
