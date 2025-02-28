Sim, é perfeitamente possível criar um script que apareça no menu de contexto do Windows para executar um `git pull` diretamente a partir do clique com o botão direito em uma pasta. Vou te guiar passo a passo para criar isso:

### Passo 1: Criar um Script Batch
Primeiro, você precisa criar um script batch que execute o comando `git pull`. Abra o Bloco de Notas e cole o seguinte código:

```batch
@echo off
cd %1
git pull
pause
```

Salve este arquivo com a extensão `.bat`, por exemplo, `git_pull.bat`. Escolha um local seguro para salvar, como `C:\Scripts\git_pull.bat`.

### Passo 2: Adicionar o Script ao Menu de Contexto
Agora, você precisa adicionar uma entrada no registro do Windows para que o script apareça no menu de contexto.

1. **Abra o Editor do Registro**:
   - Pressione `Win + R`, digite `regedit` e pressione Enter.

2. **Navegue até a chave correta**:
   - No Editor do Registro, navegue até a seguinte chave:
     ```
     HKEY_CLASSES_ROOT\Directory\Background\shell\
     ```

3. **Criar uma nova chave**:
   - Clique com o botão direito em `shell`, selecione `Novo > Chave` e nomeie-a como `GitPull`.

4. **Definir o nome que aparecerá no menu**:
   - Clique na chave `GitPull` que você acabou de criar.
   - No painel à direita, clique duas vezes em `(Padrão)` e insira o nome que você deseja que apareça no menu de contexto, por exemplo, `Git Pull`.

5. **Criar uma subchave para o comando**:
   - Clique com o botão direito na chave `GitPull`, selecione `Novo > Chave` e nomeie-a como `command`.

6. **Definir o comando a ser executado**:
   - Clique na chave `command` que você acabou de criar.
   - No painel à direita, clique duas vezes em `(Padrão)` e insira o caminho completo para o seu script batch, seguido de `"%V"`. Por exemplo:
     ```
     C:\Scripts\git_pull.bat "%V"
     ```

### Passo 3: Testar
Agora, quando você clicar com o botão direito em qualquer pasta (incluindo a raiz de um repositório Git), você verá a opção `Git Pull` no menu de contexto. Ao selecioná-la, o script executará o comando `git pull` naquela pasta.

### Considerações Finais
- **Permissões**: Certifique-se de que o script batch tenha permissão para executar comandos Git no diretório selecionado.
- **Segurança**: Tenha cuidado ao editar o registro do Windows. Sempre faça um backup antes de fazer alterações.

Com isso, você economizará tempo e esforço ao trabalhar com repositórios Git! 🚀