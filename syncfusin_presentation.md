---
marp: true
theme: ./catpuccin-mocha.css 
paginate: true
---

# Syncfusion Essential com Angular

Marcos Queiroz e Joel Jr.

---

## A Biblioteca Syncfusion (EJ2)

- **Origem:** Empresa fundada em 2001, focada no mercado corporativo.
- **Essential JS 2:** Suíte reescrita do zero em TypeScript, leve e modular.
- **Filosofia:** Agnosticismo de design. Não impõe um estilo único, adaptando-se a Material, Tailwind, Bootstrap e Fluent.
- **Comunidade e Suporte:** Possui uma documentação extremamente robusta e suporte técnico direto. Oferece licença comunitária gratuita para desenvolvedores individuais e startups.

---

## Criando o Projeto e Instalando

O ecossistema Angular facilita a integração utilizando o Angular CLI.

**1. Criando um projeto novo:**
```bash
ng new carrinho-app
cd carrinho-app
```

---

## Aplicando um Tema

A configuração do tema garante a consistência visual dos componentes. 

No arquivo `angular.json` ou importando diretamente no seu `styles.scss`:
```scss
/* Exemplo importando o tema Material globalmente */
@import '../node_modules/@syncfusion/ej2-base/styles/material.scss';
@import '../node_modules/@syncfusion/ej2-angular-grids/styles/material.scss';
```

---

## 📦 Componente: DataGrid (Tabelas)

O **Grid** é o componente mais robusto da suíte, projetado para exibir e manipular grandes volumes de dados com alta performance.

- **Recursos Principais:** Paginação, ordenação avançada e filtros.
- **Exportação:** Suporte nativo e simples para gerar PDFs e planilhas Excel.
- **Edição:** Permite CRUD completo direto na linha (inline) ou via modal.

**Instalando o pacote**
```bash
npm install @syncfusion/ej2-angular-grids --save
```

---

<style scoped>
pre { font-size: 18px; line-height: 1.2; margin: 5px 0; padding: 10px; }
p { margin: 5px 0; font-size: 24px; }
</style>

## 💻 Código: DataGrid (Carrinho)

**`carrinho.component.html`**
```html
<ejs-grid [dataSource]="itensCarrinho">
  <e-columns>
    <e-column field="produto" headerText="Produto" width="150"></e-column>
    <e-column field="qtd" headerText="Quantidade" width="100"></e-column>
    <e-column field="preco" headerText="Preço" format="C2"></e-column>
  </e-columns>
</ejs-grid>
```

**`carrinho.component.ts`**
```typescript
export class CarrinhoComponent {
  public itensCarrinho: Object[] = [
    { produto: 'Monitor Ultrawide', qtd: 1, preco: 1500.00 },
    { produto: 'Teclado Mecânico', qtd: 2, preco: 350.50 }
  ];
}
```

---

## 🎛️ Componente: Formulários e Inputs

A biblioteca oferece dezenas de controles de entrada de dados, desde os mais simples até seletores complexos, garantindo a integridade dos dados antes de irem para o backend.

- **Variedade:** `MultiSelect`, `DatePicker`, `RichTextEditor`, etc.
- **Controle Preciso:** O `NumericTextBox` evita entradas de texto inválidas e permite formatar moedas e porcentagens.
- **Integração:** Compatível 100% com os Formulários Reativos do Angular.

**Instalando o pacote**
```bash
ng add @syncfusion/ej2-angular-inputs
```

---

<style scoped>
pre { font-size: 18px; line-height: 1.2; margin: 5px 0; padding: 10px; }
p { margin: 5px 0; font-size: 24px; }
</style>

## 💻 Código: NumericTextBox (Quantidade)

**`carrinho.component.html`**
```html
<label>Quantidade:</label>
<ejs-numerictextbox 
    [value]="quantidadeItens" 
    [min]="minQtd" 
    [max]="estoqueMax" 
    format="n0">
</ejs-numerictextbox>
```

**`carrinho.component.ts`**
```typescript
export class CarrinhoComponent {
  public quantidadeItens: number = 1;
  public minQtd: number = 1;
  public estoqueMax: number = 5; // Limite máximo de compra
}
```

---

## 🚨 Componente: Modais (Dialog)

O **Dialog** exibe informações importantes ou pede confirmações ao usuário sem que ele precise sair da página atual.

- **Flexibilidade:** Pode atuar como um alerta simples ou renderizar um formulário completo dentro dele.
- **Interatividade:** Janelas podem ser redimensionadas e arrastadas pela tela (*draggable*).
- **Foco:** Opção de escurecer o fundo (overlay) para forçar a atenção do usuário no aviso.

**Instalando o pacote**
```bash
ng add @syncfusion/ej2-angular-popups
```

---

<style scoped>
pre { font-size: 18px; line-height: 1.2; margin: 5px 0; padding: 10px; }
p { margin: 5px 0; font-size: 24px; }
</style>

## 💻 Código: Dialog (Checkout)

**`carrinho.component.html`**
```html
<button ejs-button (click)="abrirModal()">Finalizar Compra</button>

<ejs-dialog [visible]="modalAberto" header="Confirmar" [isModal]="true">
    <ng-template #content>
        Tem certeza que deseja processar o pagamento no valor de R$ 2.201,00?
    </ng-template>
</ejs-dialog>
```

**`carrinho.component.ts`**
```typescript
export class CarrinhoComponent {
  public modalAberto: boolean = false;

  abrirModal(): void {
    this.modalAberto = true; // Gatilho que exibe o componente na tela
  }
}
```

---

## 📊 Componente: Gráficos (Charts)

- **Tipos de Gráficos:** Barras, Linhas, Dispersão, Pizza (Accumulation), Financeiros, etc.
- **Interatividade:** Tooltips nativas, zoom, legendas clicáveis e animações fluidas.
- **Responsividade:** Ajusta-se automaticamente ao tamanho da tela e do contêiner.

**Instalando o pacote**
```bash
ng add @syncfusion/ej2-angular-charts
```

---

<style scoped>
pre { font-size: 18px; line-height: 1.2; margin: 5px 0; padding: 10px; }
p { margin: 5px 0; font-size: 24px; }
</style>

## 💻 Código: Gráfico de Pizza (Resumo)

**`carrinho.component.html`**
```html
<ejs-accumulationchart id="grafico-custos">
    <e-accumulation-series-collection>
        <e-accumulation-series [dataSource]="dadosCusto" xName="tipo" yName="valor">
        </e-accumulation-series>
    </e-accumulation-series-collection>
</ejs-accumulationchart>
```

**`carrinho.component.ts`**
```typescript
export class CarrinhoComponent {
  public dadosCusto: Object[] = [
    { tipo: 'Subtotal dos Produtos', valor: 2201.00 },
    { tipo: 'Frete e Entrega', valor: 45.00 },
    { tipo: 'Taxas', valor: 12.00 }
  ];
}
```

---

## Como Trocar de Tema

O Syncfusion não amarra a aplicação a um único visual.

**Alternância Manual / Build:**
Basta trocar o caminho do arquivo CSS no seu `angular.json` ou `styles.scss`:
- De: `.../styles/material.css`
- Para: `.../styles/tailwind.css`

---

# Demonstração
