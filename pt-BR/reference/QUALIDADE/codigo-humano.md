# Escreva Código Humano & Não Exagere na Engenharia

> Tecnicas de Prompting: **Zero-shot** (human code) + **Directional Stimulus** (simplicidade)

---

## Parte 1: Escreva Código Humano

### O Principio Fundamental

Escreva codigo que parece ter sido escrito por um humano — nao por uma maquina geradora de templates corporativos. Codigo e comunicacao entre pessoas, nao apenas instrucoes para computadores.

### Chain-of-Thought: Por que codigo "robotico" e ruim?

1. **Aumenta carga cognitiva** - Desenvolvedores gastam mais tempo decodificando comentarios obvios
2. **Envelhece mal** — Comentarios explicativos ficam desatualizados; codigo nao mente
3. **Distorce prioridades** — Foco em documentar o obvio em vez de explicar o complexo

---

### Anti-Padroes de Codigo Robotico

#### ❌ Comentarios Corporativos Obvios

```typescript
/**
 * Button Component
 * This component renders a button element
 * @author Claude
 * @version 1.0
 * @param props - The properties for the button
 * @returns JSX.Element
 */
export const Button: React.FC<ButtonProps> = (props): JSX.Element => {
  // Check if button is disabled
  const isDisabled = props.disabled;

  // Render the button
  return (
    <button disabled={isDisabled}>
      {props.children}
    </button>
  );
};
```

#### ❌ Separacao Excessiva de Concerns Prematura

```typescript
// utils/formatting/date/formatDate.ts
// utils/formatting/date/formatTime.ts
// utils/formatting/date/constants.ts
// utils/formatting/date/types.ts

// Para uma unica funcao de formatar data!
```

#### ❌ Nomenclatura Mecanica

```typescript
interface DataInterface {}
class ManagerClass {}
type ConfigType = {}
```

---

### Padroes de Codigo Humano

#### ✅ Comentarios que Explicam o "Porque", nao o "O Que"

```typescript
// ❌ Ruim: explica o obvio
// Incrementa o contador em 1
counter++;

// ✅ Bom: explica a intencao
// Precisamos ajustar o indice porque arrays no momento X sao 0-based
// mas o sistema legado espera 1-based
counter++;
```

#### ✅ Nomes que Falam por Si

```typescript
// ❌ Ruim: precisa de comentario
function process(d: Data) { /* ... */ } // processa dados

// ✅ Bom: nome descritivo
function normalizeUserProfile(rawProfile: ApiResponse): User {
  /* ... */
}
```

#### ✅ Consistencia com Padroes do Projeto

```typescript
// Se o projeto usa:
const user = { name: 'Joao', age: 30 };

// Nao invente:
const userObj = new UserObject();
userObj.setName('Joao');
userObj.setAge(30);
```

---

### Directional Stimulus: A Pergunta Decisiva

> Se tres desenvolvedores experientes escreveriam isso da mesma forma, e assim que deve ser escrito.

---

## Parte 2: Não Exagere na Engenharia

### O Principio da Simplicidade

**Nao construa para cenarios imaginarios.** Se a solucao lida com necessidades hipoteticas futuras que ninguem pediu, simplifique. Simples e correto vence elaborado e especulativo.

### Chain-of-Thought: Sinais de Over-Engineering

1. **"E se no futuro..."** — Voce esta adivinhando requisitos
2. **Abstracoes sem uso concreto** — Interfaces para "flexibilidade" que nunca sera usada
3. **Configuracao excessiva** — Sistemas de plugin para 2 casos de uso
4. **Otimizacao prematura** — Otimizar codigo que ainda nao e gargalo

---

### Anti-Padroes de Over-Engineering

#### ❌ Sistema de Plugins para Codigo Interno

```typescript
// Para adicionar UMA validacao de email?
interface ValidatorPlugin {
  name: string;
  validate: (value: unknown) => ValidationResult;
}

class ValidationRegistry {
  private plugins = new Map<string, ValidatorPlugin>();

  register(plugin: ValidatorPlugin) { /* ... */ }
  validate(field: string, value: unknown) { /* ... */ }
}

// VS
const isEmail = (s: string) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(s);
```

#### ❌ Factory Factories

```typescript
abstract class AbstractFactory<T> {
  abstract create(): T;
}

class ServiceFactory extends AbstractFactory<Service> {
  create() { return new Service(); }
}

// VS
const service = new Service();
```

#### ❌ Configuracao Extensiva para Valores Padrao

```typescript
const config = {
  database: {
    connection: {
      pool: {
        min: process.env.DB_POOL_MIN ? parseInt(process.env.DB_POOL_MIN) : 2,
        max: process.env.DB_POOL_MAX ? parseInt(process.env.DB_POOL_MAX) : 10,
        timeout: process.env.DB_TIMEOUT ? parseInt(process.env.DB_TIMEOUT) : 30000,
        // ... 20 mais opcoes
      }
    }
  }
};
```

---

### Directional Stimulus em Acao: Perguntas Rapidas

Antes de adicionar complexidade, pergunte:

| Pergunta | Se a resposta for... | Acao |
|----------|---------------------|------|
| Alguem pediu isso? | Nao | Nao implemente |
| Vai ser usado nos proximos 30 dias? | Nao | Nao implemente |
| Simplificar quebraria algo existente? | Nao | Simplifique |
| Tres devs experientes fariam assim? | Nao | Reconsidere |

---

### Exemplos Comparativos

#### Cenario: Validar formulario de login

```typescript
// ❌ Over-Engineered
class ValidationStrategy {
  constructor(private rules: ValidationRule[]) {}

  async execute<T>(data: T): Promise<ValidationResult<T>> {
    const results = await Promise.all(
      this.rules.map(rule => rule.validate(data))
    );
    return this.aggregate(results);
  }

  private aggregate(results: RuleResult[]) { /* ... */ }
}

// ✅ Simples e Direto
function validateLogin(email: string, password: string): string | null {
  if (!email.includes('@')) return 'Email invalido';
  if (password.length < 6) return 'Senha muito curta';
  return null;
}
```

---

## Resumo: O Equilibrio

| Aspecto | Codigo Humano | Nao Over-Engineer |
|---------|--------------|-------------------|
| **Foco** | Legibilidade | Simplicidade |
| **Evita** | Roboticismo | Complexidade especulativa |
| **Pergunta-chave** | "Tres devs fariam assim?" | "Alguem pediu isso?" |
| **Direcao** | Clareza sobre ceremonial | Funcional sobre abstrato |

> **Regra final**: Codigo deve ser tao simples quanto possivel, mas nao mais simples. A intencao deve ser clara a primeira leitura.
