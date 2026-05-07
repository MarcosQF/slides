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
@import '@syncfusion/ej2-base/styles/material.css';
@import '@syncfusion/ej2-grids/styles/material.css';
@import '@syncfusion/ej2-inputs/styles/material.css';
@import '@syncfusion/ej2-buttons/styles/material.css';
@import '@syncfusion/ej2-popups/styles/material.css';
```

---

## Componente: DataGrid (Tabelas)

O **Grid** é o componente mais robusto da suíte, projetado para exibir e manipular grandes volumes de dados com alta performance.

- **Recursos Principais:** Paginação, ordenação avançada e filtros.

**Instalando o pacote**
```bash
npm install @syncfusion/ej2-angular-grids --save
```

---

<style scoped>
pre { font-size: 18px; line-height: 1.2; margin: 5px 0; padding: 10px; }
p { margin: 5px 0; font-size: 24px; }
</style>

## 💻 Código: DataGrid 

**`component.html`**
```html
<ejs-grid [dataSource]="itensCarrinho" [allowFiltering]="true">
  <e-columns>
    <e-column field="produto" headerText="Produto" width="150"></e-column>
    <e-column field="qtd" headerText="Quantidade" width="100"></e-column>
    <e-column field="preco" headerText="Preço" format="C2"></e-column>
  </e-columns>
</ejs-grid>
```

**`component.ts`**
```typescript
import { GridModule, FilterService } from '@syncfusion/ej2-angular-grids';

export class CarrinhoComponent {
  public itensCarrinho: Object[] = [
    { produto: 'Monitor Ultrawide', qtd: 1, preco: 1500.00 },
    { produto: 'Teclado Mecânico', qtd: 2, preco: 350.50 }
  ];
}
```

---

## Componente: Formulários e Inputs

A biblioteca oferece dezenas de controles de entrada de dados, desde os mais simples até seletores complexos, garantindo a integridade dos dados antes de irem para o backend.

- **Variedade:** `MultiSelect`, `DatePicker`, `RichTextEditor`, etc.
- **Controle Preciso:** O `NumericTextBox` evita entradas de texto inválidas e permite formatar moedas e porcentagens.

**Instalando o pacote**
```bash
npm install @syncfusion/ej2-angular-inputs --save
```

---

<style scoped>
pre { font-size: 18px; line-height: 1.2; margin: 5px 0; padding: 10px; }
p { margin: 5px 0; font-size: 24px; }
</style>

## Código: NumericTextBox

**`component.html`**
```html
<label>Quantidade:</label>
<ejs-numerictextbox 
    [value]="quantidadeItens" 
    [min]="minQtd" 
    [max]="estoqueMax" 
    format="n0">
</ejs-numerictextbox>
```

**`component.ts`**
```typescript
import { NumericTextBoxModule } from '@syncfusion/ej2-angular-inputs';

export class CarrinhoComponent {
  public quantidadeItens: number = 1;
  public minQtd: number = 1;
  public estoqueMax: number = 5; // Limite máximo de compra
}
```

---

## Componente: Modais (Dialog)

O **Dialog** exibe informações importantes ou pede confirmações ao usuário sem que ele precise sair da página atual.

- **Flexibilidade:** Pode atuar como um alerta simples ou renderizar um formulário completo dentro dele.
- **Interatividade:** Janelas podem ser redimensionadas e arrastadas pela tela (*draggable*).
- **Foco:** Opção de escurecer o fundo (overlay) para forçar a atenção do usuário no aviso.

**Instalando o pacote**
```bash
npm install @syncfusion/ej2-angular-buttons @syncfusion/ej2-angular-popups --save
```

---
<style scoped>
pre { font-size: 18px; line-height: 1.2; margin: 5px 0; padding: 10px; }
p { margin: 5px 0; font-size: 24px; }
</style>
#### Código: Dialog
**`component.html`**
```html
<button ejs-button (click)="abrirModal()">Finalizar Compra</button>
<ejs-dialog [(visible)]="modalAberto" header="Confirmar" [isModal]="true" [showCloseIcon]="true" width="400px">
    <ng-template #content>
        Tem certeza que deseja processar o pagamento no valor de R$ 2.201,00?
    </ng-template>
    <ng-template #footerTemplate>
        <button ejs-button (click)="fecharModal()">Cancelar</button>
        <button ejs-button cssClass="e-primary" (click)="fecharModal()">Confirmar</button>
    </ng-template>
</ejs-dialog>
```
**`component.ts`**
```typescript
import { DialogModule } from '@syncfusion/ej2-angular-popups';
import { ButtonModule } from '@syncfusion/ej2-angular-buttons';
export class CarrinhoComponent {
  public modalAberto: boolean = false;
  abrirModal(): void {
    this.modalAberto = true;
  }
  fecharModal(): void {
    this.modalAberto = false;
  }
}
```

---

## Componente: Gráficos (Charts)

- **Tipos de Gráficos:** Barras, Linhas, Dispersão, Pizza (Accumulation), Financeiros, etc.
- **Interatividade:** Tooltips nativas, zoom, legendas clicáveis e animações fluidas.
- **Responsividade:** Ajusta-se automaticamente ao tamanho da tela e do contêiner.

**Instalando o pacote**
```bash
npm install @syncfusion/ej2-angular-charts --save
```

---

<style scoped>
pre { font-size: 18px; line-height: 1.2; margin: 5px 0; padding: 10px; }
p { margin: 5px 0; font-size: 24px; }
</style>

### Código: Gráfico de Pizza 

**`component.html`**
```html
<ejs-accumulationchart id="grafico-custos">
    <e-accumulation-series-collection>
        <e-accumulation-series [dataSource]="dadosCusto" xName="tipo" yName="valor">
        </e-accumulation-series>
    </e-accumulation-series-collection>
</ejs-accumulationchart>
```

**`component.ts`**
```typescript
import {
  AccumulationChartModule,
  PieSeriesService,
  AccumulationLegendService,
  AccumulationTooltipService
} from '@syncfusion/ej2-angular-charts';

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
Basta trocar o caminho do arquivo CSS no seu`styles.scss`:
```scss
@import '@syncfusion/ej2-base/styles/tailwind-dark.css';
@import '@syncfusion/ej2-grids/styles/tailwind-dark.css';
@import '@syncfusion/ej2-inputs/styles/tailwind-dark.css';
@import '@syncfusion/ej2-buttons/styles/tailwind-dark.css';
@import '@syncfusion/ej2-popups/styles/tailwind-dark.css';
```
---

# Demonstração
