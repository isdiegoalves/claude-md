# Siga Referências, Não Descrições

> Tecnica: **Few-shot Prompting** - Aprendizado por exemplos/referencias

---

## O Principio

Quando o usuario aponta para codigo existente como referencia:
1. **Estude minuciosamente** antes de construir
2. **Combine padroes exatamente** - nao reinvente
3. **Codigo funcionando > Descricao em ingles**

---

## Few-shot por Referencia

### Como Aprender do Codigo Existente

```typescript
// EXEMPLO (referencia fornecida):
// UserService.ts existente
export class UserService {
  async getUser(id: string): Promise<User> {
    const response = await this.api.get(`/users/${id}`);
    return response.data;
  }
}

// TAREFA: Criar ProductService

// ✅ CORRETO - Segue padrao da referencia:
export class ProductService {
  async getProduct(id: string): Promise<Product> {
    const response = await this.api.get(`/products/${id}`);
    return response.data;
  }
}

// ❌ ERRADO - Inventa padrao diferente:
export const fetchProduct = async (id: string) => {
  return axios.get(`/api/products/${id}`);
};
```

---

## Checklist de Referencia

Antes de implementar:
- [ ] Estudei o codigo de referencia completo
- [ ] Identifiquei os padroes usados
- [ ] Notei convencoes de naming
- [ ] Observei estrutura de arquivos
- [ ] Repliquei os padroes na nova implementacao

---

## Sinais de Referencia

| Sinal | Significado | Acao |
|-------|-------------|------|
| "Como em [arquivo]" | Use como modelo | Leia e siga o padrao |
| "Seguindo o padrao de..." | Consistencia obrigatoria | Estude o referencial |
| "Similar a [funcao]" | Adaptacao controlada | Copie estrutura, adapte logica |
| "No estilo do projeto" | Convencoes existentes | Analise multiplos exemplos |

---

## Exemplo de Few-shot em Acao

```markdown
Usuario: "Crie um novo hook useAuth, seguindo o padrao do useUser"

Acao Few-shot:
1. Leia useUser.ts completamente
2. Note:
   - Estrutura: export function useUser() { ... }
   - Retorno: { user, loading, error }
   - Interno: useState, useEffect, try/catch
3. Replique estrutura em useAuth.ts:
   - export function useAuth() { ... }
   - Retorno: { auth, loading, error }
   - Mesmo padrao de gerenciamento de estado
```
