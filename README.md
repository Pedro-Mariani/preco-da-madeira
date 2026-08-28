# Preços · Madeireiras

Formulário para lançar preços (forro, parede, frete) de madeireiras, com dados salvos no Firebase Firestore.

## Como publicar

### 1. Subir para o GitHub
1. Crie um repositório novo em github.com (pode ser privado)
2. Faça upload do arquivo `index.html` que está nesta pasta (pela interface web do GitHub: "Add file" → "Upload files")

### 2. Conectar na Vercel
1. Acesse vercel.com e faça login (pode usar sua conta do GitHub)
2. Clique em "Add New" → "Project" → "Import Git Repository"
3. Selecione o repositório que você acabou de criar
4. Não precisa mudar nenhuma configuração — é um site estático (HTML puro). Clique em "Deploy"
5. Em alguns segundos a Vercel te dá uma URL pública (ex: `precos-madeireiras.vercel.app`)

### 3. Atualizações futuras
Sempre que quiser mudar algo no formulário (cores, campos, lista de madeireiras), edite o `index.html` e suba a alteração pro GitHub — a Vercel atualiza o site sozinha a cada novo commit.

## Importante: travar a segurança do Firestore

Por enquanto o banco está em "modo de teste", que expira em 30 dias e permite que qualquer pessoa leia/escreva os dados diretamente (não pelo site). Antes de expirar, vá em:

Firebase Console → Firestore Database → aba "Regras" e troque pelo seguinte:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /precos/{docId} {
      allow read: if true;
      allow write: if true;
    }
  }
}
```

Essa regra libera leitura e escrita pra qualquer pessoa que tenha a URL do site (sem exigir login) — é o mais simples para uso em equipe pequena. Se um dia quiser mais controle (exigir senha, por exemplo), me avise que ajustamos.
