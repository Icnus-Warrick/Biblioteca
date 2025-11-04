# 🚀 Guia Rápido - Internacionalização (i18n)

## ⚡ Uso Básico

### 1. Importar e usar mensagens

```java
import br.com.warrick.biblioteca.util.I18nManager;

// Obter mensagem traduzida
String titulo = I18nManager.msg("app.title");
String botao = I18nManager.msg("login.button");

// Usar em componentes Swing
JLabel label = new JLabel(I18nManager.msg("login.username"));
JButton button = new JButton(I18nManager.msg("button.save"));
```

### 2. Trocar idioma

```java
I18nManager i18n = I18nManager.getInstance();

// Para Português
i18n.setLocale(I18nManager.LOCALE_PT_BR);

// Para Inglês
i18n.setLocale(I18nManager.LOCALE_EN_US);

// Alternar entre idiomas
i18n.toggleLanguage();
```

### 3. Adicionar seletor de idioma na UI

```java
import br.com.warrick.biblioteca.util.LanguageSwitcher;

JPanel panel = new JPanel();
LanguageSwitcher switcher = new LanguageSwitcher();
panel.add(switcher);
```

### 4. Usar painel de configurações completo

```java
import br.com.warrick.biblioteca.view.SettingsPanel;

JFrame frame = new JFrame();
SettingsPanel settings = new SettingsPanel();
frame.add(settings);
```

---

## 🎯 Exemplos Práticos

### Exemplo 1: Atualizar UI quando idioma mudar

```java
import br.com.warrick.biblioteca.util.I18nManager;
import br.com.warrick.biblioteca.util.LanguageChangeListener;

public class MinhaJanela extends JFrame {
    private JLabel titleLabel;
    private JButton saveButton;
    
    public MinhaJanela() {
        initComponents();
        setupI18n();
    }
    
    private void initComponents() {
        titleLabel = new JLabel();
        saveButton = new JButton();
        // ... adicionar componentes
    }
    
    private void setupI18n() {
        // Atualizar textos inicialmente
        updateTexts();
        
        // Registrar listener para mudanças de idioma
        I18nManager.getInstance().addLanguageChangeListener(
            (oldLocale, newLocale) -> updateTexts()
        );
    }
    
    private void updateTexts() {
        titleLabel.setText(I18nManager.msg("app.title"));
        saveButton.setText(I18nManager.msg("button.save"));
        setTitle(I18nManager.msg("app.title"));
    }
}
```

### Exemplo 2: Mensagens com parâmetros

```java
// Adicionar no arquivo .properties:
// user.greeting=Olá, %s! Você tem %d mensagens.

// Usar no código:
String nome = "João";
int mensagens = 5;
String texto = I18nManager.msg("user.greeting", nome, mensagens);
// Resultado: "Olá, João! Você tem 5 mensagens."
```

### Exemplo 3: Verificar idioma atual

```java
I18nManager i18n = I18nManager.getInstance();

if (i18n.isPortuguese()) {
    // Código específico para português
    System.out.println("Idioma: Português");
}

if (i18n.isEnglish()) {
    // Código específico para inglês
    System.out.println("Language: English");
}

// Obter locale atual
Locale current = i18n.getCurrentLocale();
System.out.println("Locale: " + current);
```

---

## 📝 Chaves Mais Usadas

### Aplicação
- `app.title` - Título da aplicação
- `app.loading.title` - Título de carregamento
- `app.success` - Mensagem de sucesso

### Login
- `login.username` - Usuário
- `login.password` - Senha
- `login.button` - Botão de login
- `login.error.invalid` - Erro de login

### Botões
- `button.ok` - OK
- `button.cancel` - Cancelar
- `button.save` - Salvar
- `button.delete` - Excluir
- `button.close` - Fechar

### Mensagens
- `message.welcome` - Bem-vindo
- `message.loading` - Carregando
- `message.saving` - Salvando
- `error.generic` - Erro genérico
- `success.title` - Título de sucesso

### Biblioteca
- `library.books` - Livros
- `library.search` - Pesquisar
- `library.add.book` - Adicionar livro
- `library.no.books` - Nenhum livro encontrado

### Validações
- `validation.email.invalid` - E-mail inválido
- `validation.password.weak` - Senha fraca
- `validation.field.required` - Campo obrigatório

---

## 🧪 Testar o Sistema

### Executar exemplo interativo

```bash
# Compilar e executar o exemplo
mvn compile
mvn exec:java -Dexec.mainClass="br.com.warrick.biblioteca.util.I18nExample"
```

### Executar painel de configurações

```bash
mvn exec:java -Dexec.mainClass="br.com.warrick.biblioteca.view.SettingsPanel"
```

---

## ➕ Adicionar Novas Mensagens

1. Abra os 3 arquivos `.properties` em `src/main/resources/`:
   - `messages.properties` (padrão)
   - `messages_pt_BR.properties` (português)
   - `messages_en_US.properties` (inglês)

2. Adicione a mesma chave nos 3 arquivos com traduções diferentes:

**messages_pt_BR.properties:**
```properties
minha.mensagem=Olá, Mundo!
```

**messages_en_US.properties:**
```properties
minha.mensagem=Hello, World!
```

3. Use no código:
```java
String msg = I18nManager.msg("minha.mensagem");
```

---

## 🔧 Dicas e Boas Práticas

### ✅ Faça
- Use chaves descritivas: `login.button.submit` em vez de `btn1`
- Organize por contexto: `login.`, `error.`, `button.`
- Traduza TODAS as chaves em TODOS os idiomas
- Use i18n para TODOS os textos visíveis
- Teste em ambos os idiomas

### ❌ Evite
- Hardcoding de textos: `new JLabel("Login")` ❌
- Chaves genéricas: `msg1`, `text2` ❌
- Deixar chaves sem tradução ❌
- Misturar idiomas no código ❌

---

## 📚 Arquivos Criados

### Classes Java
- `I18nManager.java` - Gerenciador principal
- `LanguageChangeListener.java` - Interface para listeners
- `LanguageSwitcher.java` - Componente seletor de idioma
- `SettingsPanel.java` - Painel de configurações completo
- `I18nExample.java` - Exemplo interativo

### Recursos
- `messages.properties` - Mensagens padrão
- `messages_pt_BR.properties` - Português do Brasil
- `messages_en_US.properties` - Inglês dos EUA

### Documentação
- `I18N_README.md` - Documentação completa
- `QUICK_START_I18N.md` - Este guia rápido

---

## 🆘 Problemas Comuns

### Mensagem aparece como `!chave!`
**Causa:** Chave não existe nos arquivos `.properties`  
**Solução:** Adicione a chave em todos os arquivos `.properties`

### Idioma não muda
**Causa:** UI não está sendo atualizada após mudança  
**Solução:** Use `LanguageChangeListener` para atualizar a UI

### Caracteres especiais aparecem errados
**Causa:** Encoding incorreto  
**Solução:** Salve os arquivos `.properties` em UTF-8

---

## 📞 Próximos Passos

1. ✅ Execute o exemplo: `I18nExample.java`
2. ✅ Teste o painel de configurações: `SettingsPanel.java`
3. ✅ Adicione i18n nas suas classes existentes
4. ✅ Adicione novas mensagens conforme necessário
5. ✅ Teste em ambos os idiomas

---

**Documentação completa:** Veja `I18N_README.md`  
**Suporte:** Entre em contato com a equipe de desenvolvimento
