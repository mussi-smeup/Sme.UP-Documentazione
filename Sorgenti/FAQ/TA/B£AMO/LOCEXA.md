### **Che differenza c'è tra asse e serie?**

// Perchè zzzz

### **Perchè yyy?**

// Perchè bbbb

### **Posso fare un grafico di più tipologie?**

Si, e possibile usare più tipologie di grafico, grazie all'attributo Typ
Impostando (ad esempio) questo attributo a Typ="VBAR|LINE", la prima serie verra disegnata con un diagramma a barre verticali, la seconda come una linea.

### **I dati devono essere già sommati?**

No. I dati appartenenti alla stessa serie vengono sommati in automatico. Per evitare questo comportamento, bisogna utilizzare l'attributo di setup GroupData="No"

### **Come si gestiscono le informazioni temporali?**

I grafici gestiscono automaticamente i dati oggettizzati come temporali, ad esempio date (D8\*YYMD) o ore (I12, I13...)

### **Come si fa un grafico dinamico?**

Utilizzando l'attributo di setup Reload="X".
X rappresenta ogni quanti secondi il grafico deve ricaricare i dati :  ad esempio, con Reload="2" i dati verranno aggiornati ogni 2 secondi.

### **Skill di Test**

// test
