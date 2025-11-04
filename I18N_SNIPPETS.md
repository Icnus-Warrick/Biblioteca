# 📋 Snippets de Código - i18n

Copie e cole estes snippets para usar i18n rapidamente no seu projeto.

---

## 🎨 Componentes Swing com i18n

### JLabel
```java
JLabel label = new JLabel(I18nManager.msg("login.username"));
```

### JButton
```java
JButton button = new JButton(I18nManager.msg("button.save"));
button.addActionListener(e -> {
    JOptionPane.showMessageDialog(null, 
        I18nManager.msg("message.saving"));
});
```

### JTextField com placeholder
```java
JTextField field = new JTextField();
field.setToolTipText(I18nManager.msg("form.required"));
```

### JOptionPane
```java
// Mensagem de erro
JOptionPane.showMessageDialog(null,
    I18nManager.msg("error.database"),
    I18nManager.msg("error.title"),
    JOptionPane.ERROR_MESSAGE);

// Mensagem de sucesso
JOptionPane.showMessageDialog(null,
    I18nManager.msg("success.login"),
    I18nManager.msg("success.title"),
    JOptionPane.INFORMATION_MESSAGE);

// Confirmação
int result = JOptionPane.showConfirmDialog(null,
    I18nManager.msg("confirm.delete"),
    I18nManager.msg("confirm.title"),
    JOptionPane.YES_NO_OPTION);
```

### JMenu
```java
JMenuBar menuBar = new JMenuBar();
JMenu fileMenu = new JMenu(I18nManager.msg("menu.file"));
JMenuItem exitItem = new JMenuItem(I18nManager.msg("menu.exit"));
fileMenu.add(exitItem);
menuBar.add(fileMenu);
```

---

## 🔄 Atualização Dinâmica de UI

### Painel que atualiza automaticamente
```java
public class MyPanel extends JPanel {
    private JLabel titleLabel;
    private JButton saveButton;
    private JButton cancelButton;
    
    public MyPanel() {
        initComponents();
        setupI18n();
    }
    
    private void initComponents() {
        titleLabel = new JLabel();
        saveButton = new JButton();
        cancelButton = new JButton();
        
        // Layout e outros componentes...
        add(titleLabel);
        add(saveButton);
        add(cancelButton);
    }
    
    private void setupI18n() {
        // Atualizar textos inicialmente
        updateTexts();
        
        // Registrar listener para mudanças de idioma
        I18nManager.getInstance().addLanguageChangeListener(
            (oldLocale, newLocale) -> {
                updateTexts();
                System.out.println("Idioma alterado: " + 
                    oldLocale + " -> " + newLocale);
            }
        );
    }
    
    private void updateTexts() {
        titleLabel.setText(I18nManager.msg("app.title"));
        saveButton.setText(I18nManager.msg("button.save"));
        cancelButton.setText(I18nManager.msg("button.cancel"));
        
        // Atualizar tooltips
        saveButton.setToolTipText(I18nManager.msg("button.save"));
        
        revalidate();
        repaint();
    }
}
```

### JFrame que atualiza título
```java
public class MyFrame extends JFrame {
    
    public MyFrame() {
        initComponents();
        setupI18n();
    }
    
    private void setupI18n() {
        updateTitle();
        
        I18nManager.getInstance().addLanguageChangeListener(
            (oldLocale, newLocale) -> updateTitle()
        );
    }
    
    private void updateTitle() {
        setTitle(I18nManager.msg("app.title"));
    }
}
```

---

## 🎛️ Seletor de Idioma

### Seletor simples com ComboBox
```java
JComboBox<String> languageCombo = new JComboBox<>(new String[]{
    "🇧🇷 Português",
    "🇺🇸 English"
});

languageCombo.addActionListener(e -> {
    int index = languageCombo.getSelectedIndex();
    I18nManager i18n = I18nManager.getInstance();
    
    if (index == 0) {
        i18n.setLocale(I18nManager.LOCALE_PT_BR);
    } else {
        i18n.setLocale(I18nManager.LOCALE_EN_US);
    }
});
```

### Botão de alternância
```java
JButton toggleButton = new JButton("PT/EN");
toggleButton.addActionListener(e -> {
    I18nManager.getInstance().toggleLanguage();
    
    // Atualizar texto do botão
    if (I18nManager.getInstance().isPortuguese()) {
        toggleButton.setText("PT ✓");
    } else {
        toggleButton.setText("EN ✓");
    }
});
```

### Menu de idiomas
```java
JMenu languageMenu = new JMenu(I18nManager.msg("settings.language"));

JMenuItem ptItem = new JMenuItem("🇧🇷 Português");
ptItem.addActionListener(e -> 
    I18nManager.getInstance().setLocale(I18nManager.LOCALE_PT_BR));

JMenuItem enItem = new JMenuItem("🇺🇸 English");
enItem.addActionListener(e -> 
    I18nManager.getInstance().setLocale(I18nManager.LOCALE_EN_US));

languageMenu.add(ptItem);
languageMenu.add(enItem);
```

---

## 📝 Validação com i18n

### Validar campo obrigatório
```java
public boolean validateField(JTextField field) {
    if (field.getText().trim().isEmpty()) {
        JOptionPane.showMessageDialog(null,
            I18nManager.msg("validation.field.required"),
            I18nManager.msg("error.title"),
            JOptionPane.ERROR_MESSAGE);
        return false;
    }
    return true;
}
```

### Validar email
```java
public boolean validateEmail(String email) {
    String emailRegex = "^[A-Za-z0-9+_.-]+@(.+)$";
    if (!email.matches(emailRegex)) {
        JOptionPane.showMessageDialog(null,
            I18nManager.msg("validation.email.invalid"),
            I18nManager.msg("error.title"),
            JOptionPane.ERROR_MESSAGE);
        return false;
    }
    return true;
}
```

### Validar senha
```java
public boolean validatePassword(String password) {
    if (password.length() < 6) {
        JOptionPane.showMessageDialog(null,
            I18nManager.msg("validation.password.weak"),
            I18nManager.msg("error.title"),
            JOptionPane.ERROR_MESSAGE);
        return false;
    }
    return true;
}
```

---

## 🔔 Notificações e Mensagens

### Mensagem de carregamento
```java
JLabel loadingLabel = new JLabel(I18nManager.msg("message.loading"));
// Adicionar ao painel
```

### Barra de progresso com mensagem
```java
JProgressBar progressBar = new JProgressBar();
JLabel statusLabel = new JLabel(I18nManager.msg("message.processing"));

// Atualizar durante processamento
SwingWorker<Void, Integer> worker = new SwingWorker<>() {
    @Override
    protected Void doInBackground() {
        statusLabel.setText(I18nManager.msg("message.saving"));
        // Processar...
        return null;
    }
    
    @Override
    protected void done() {
        statusLabel.setText(I18nManager.msg("success.title"));
    }
};
worker.execute();
```

---

## 🗂️ Tabelas com i18n

### Cabeçalhos de tabela
```java
String[] columnNames = {
    I18nManager.msg("form.title"),
    I18nManager.msg("form.author"),
    I18nManager.msg("form.description")
};

DefaultTableModel model = new DefaultTableModel(columnNames, 0);
JTable table = new JTable(model);
```

### Atualizar cabeçalhos dinamicamente
```java
public void updateTableHeaders(JTable table) {
    TableColumnModel columnModel = table.getColumnModel();
    columnModel.getColumn(0).setHeaderValue(I18nManager.msg("form.title"));
    columnModel.getColumn(1).setHeaderValue(I18nManager.msg("form.author"));
    columnModel.getColumn(2).setHeaderValue(I18nManager.msg("form.description"));
    table.getTableHeader().repaint();
}
```

---

## 🎯 Diálogos Personalizados

### Diálogo de confirmação
```java
public boolean showConfirmDialog(String messageKey) {
    int result = JOptionPane.showConfirmDialog(
        null,
        I18nManager.msg(messageKey),
        I18nManager.msg("confirm.title"),
        JOptionPane.YES_NO_OPTION,
        JOptionPane.QUESTION_MESSAGE
    );
    return result == JOptionPane.YES_OPTION;
}

// Uso:
if (showConfirmDialog("confirm.delete")) {
    // Executar exclusão
}
```

### Diálogo de entrada
```java
public String showInputDialog(String promptKey) {
    return JOptionPane.showInputDialog(
        null,
        I18nManager.msg(promptKey),
        I18nManager.msg("app.title"),
        JOptionPane.QUESTION_MESSAGE
    );
}
```

---

## 🧩 Classe Utilitária

### Helper para diálogos i18n
```java
public class I18nDialogs {
    
    public static void showError(String messageKey) {
        JOptionPane.showMessageDialog(null,
            I18nManager.msg(messageKey),
            I18nManager.msg("error.title"),
            JOptionPane.ERROR_MESSAGE);
    }
    
    public static void showSuccess(String messageKey) {
        JOptionPane.showMessageDialog(null,
            I18nManager.msg(messageKey),
            I18nManager.msg("success.title"),
            JOptionPane.INFORMATION_MESSAGE);
    }
    
    public static boolean confirm(String messageKey) {
        int result = JOptionPane.showConfirmDialog(null,
            I18nManager.msg(messageKey),
            I18nManager.msg("confirm.title"),
            JOptionPane.YES_NO_OPTION);
        return result == JOptionPane.YES_OPTION;
    }
}

// Uso:
I18nDialogs.showError("error.database");
I18nDialogs.showSuccess("success.login");
if (I18nDialogs.confirm("confirm.delete")) {
    // Executar ação
}
```

---

## 🎨 Temas e Estilos

### Aplicar tema com mensagens i18n
```java
public void applyTheme() {
    try {
        UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName());
        SwingUtilities.updateComponentTreeUI(this);
        
        JOptionPane.showMessageDialog(this,
            I18nManager.msg("settings.applied"),
            I18nManager.msg("success.title"),
            JOptionPane.INFORMATION_MESSAGE);
    } catch (Exception e) {
        JOptionPane.showMessageDialog(this,
            I18nManager.msg("error.generic"),
            I18nManager.msg("error.title"),
            JOptionPane.ERROR_MESSAGE);
    }
}
```

---

## 💡 Dicas Finais

### Criar constantes para chaves frequentes
```java
public class I18nKeys {
    // Botões
    public static final String BTN_SAVE = "button.save";
    public static final String BTN_CANCEL = "button.cancel";
    public static final String BTN_OK = "button.ok";
    
    // Erros
    public static final String ERR_DATABASE = "error.database";
    public static final String ERR_GENERIC = "error.generic";
    
    // Uso:
    String msg = I18nManager.msg(I18nKeys.BTN_SAVE);
}
```

### Método helper para componentes
```java
public static JButton createI18nButton(String key, ActionListener action) {
    JButton button = new JButton(I18nManager.msg(key));
    button.addActionListener(action);
    return button;
}

// Uso:
JButton saveBtn = createI18nButton("button.save", e -> save());
```

---

**Mais exemplos:** Veja `I18nExample.java` e `SettingsPanel.java`
