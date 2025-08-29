# Vello — Firestore Kit (pronto pra deploy)

## Como usar
1. Descompacte o zip dentro do seu projeto **Firebase** (raiz).
2. Garanta que você tem o Firebase CLI:
   ```bash
   npm i -g firebase-tools
   firebase login
   ```
3. (Se ainda não fez) inicialize o projeto:
   ```bash
   firebase init firestore functions   # TypeScript
   ```
4. Deploy de regras, índices e functions:
   ```bash
   firebase deploy --only firestore,functions
   ```
5. Configure **TTL** (Console → Firestore → Settings → Time-to-Live) no campo `expiresAt` de:
   - `notificacoes_motorista`
   - `notificacoes_passageiro`
   - `compartilhamento_viagem`

### Scripts
- `scripts/seed.ts` — popula dados demo (requer credencial do Admin ou rodar em ambiente com permissão):
  ```bash
  # Exemplo (dentro da pasta raiz do seu projeto com credenciais de admin disponíveis)
  npx ts-node scripts/seed.ts
  ```

### Observações
- Chat foi modelado como **subcoleção**: `corridas/{id}/mensagens/{msgId}` para escala e custo baixo.
- **Geo**: use geohash + bounds no app (ex.: `geofire-common`), campo `localizacaoAtual.geohash` está indexado.
- Regras utilizam `customClaims` (`tipo = passageiro|motorista|admin`).

Happy shipping. 🏁
