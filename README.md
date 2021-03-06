# SSIS_Email
Como Enviar Email via **Integration Services**

# Criando as Variaveis 
1 - Cliquei no Icone de **Variavel** (onde está mostrando na imagem) <br />
2 - Clique em Criar uma **Variavel** (onde está mostrando na imagem) <br />
3 - De um nome para sua variavel do tipo **String** <br />
4 - O valor da variavel sera o **Email** Ex:(teste@teste.com.br) <br />
5 - Crie outra variavel  do tipo **String**  <br />
6 - O valor da variavel será a **senha** do email Ex:(teste)<br />
![alt text](https://github.com/Lmanoel1994/SSIS_Email/blob/master/pictures/1.png) <br />



# Configuando o componente Tarefa Script 
7 - Selecione uma **Tarefa Script** e jogue na tela <br />
8 - Clique duas vezes no componente para editar as configurações  <br />
9 - Em **ReadOnlyVariables** clique no **[...]** <br />
![alt text](https://github.com/Lmanoel1994/SSIS_Email/blob/master/pictures/2.png) <br />


# Selecionando as Variaveis 
10 -  Irá abri uma Janela na qual terá que seleciona as variaveis criadas **(Email, Senha)** <br />
![alt text](https://github.com/Lmanoel1994/SSIS_Email/blob/master/pictures/3.png) <br />

# Editando o Script
11 - Clique em **Editar Script ** <br />
![alt text](https://github.com/Lmanoel1994/SSIS_Email/blob/master/pictures/4.png) <br />


# Criando o Componente 
12 - Copie o Script <br />
```
using System;
using System.Net;
using System.Net.Mail;
#endregion
namespace ST_54b089ce909345e09fd19be14c685402{
	[Microsoft.SqlServer.Dts.Tasks.ScriptTask.SSISScriptTaskEntryPointAttribute]
    public partial class ScriptMain : Microsoft.SqlServer.Dts.Tasks.ScriptTask.VSTARTScriptObjectModelBase{
        public void Main(){
            String Email = Dts.Variables["Email"].Value.ToString(); 
            String Senha = Dts.Variables["Senha"].Value.ToString(); 
            SmtpClient cliente = new SmtpClient();
            cliente.Host = "smtp";
            cliente.Port = 587; 
            cliente.EnableSsl = true;
            NetworkCredential MeuEmail = new NetworkCredential(Email, Senha);
            cliente.Credentials = MeuEmail;
            var body = "<h1> Cabeçario  </h1>" +  
               "<p> Corpo do Email \n </p>" ; 
            MailMessage message = new MailMessage();
            message.IsBodyHtml = true;
            message.From = new MailAddress(Email, "Titulo"); 
            message.To.Add(new MailAddress("teste@teste.com.nr"));
            message.CC.Add(new MailAddress("teste@tteste.com.br")); 
            message.Subject = "Assunto"; 
            message.Body = body;
            cliente.Send(message);
            Dts.TaskResult = (int)ScriptResults.Success;}
        #region ScriptResults declaration
        enum ScriptResults{
            Success = Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success,
            Failure = Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Failure};
        #endregion
    }}
```
 <br />

13 - Adicione as seguintes bibliotecas  <br />
**system** <br />
**System.Net** <br />
**System.Net.Mail** <br />

14 - Adicione as variaveis **Email e Senha** <br />

15 - Adicione o **SMTP** do seu email no meu caso estou usando o Gmail <br />

16 - Adicione as **credenciais** do email  <br />

17 - Editando o Email <br />
**Escreva o Cabecario do Email**  <br />
**A mensagem que gostaria de enviar** <br />
**Titulo da Mensagem** <br />
**Email do destinatio** <br />
**Email de quem deseja deixar em copia** <br />
**Assunto do Email** <br />
Feito isso Salve o Script e feche a janela  <br />
![alt text](https://github.com/Lmanoel1994/SSIS_Email/blob/master/pictures/5.png) <br />

# Executando o Componente
18 - Execute o seu pacote  <br />
![alt text](https://github.com/Lmanoel1994/SSIS_Email/blob/master/pictures/6.png) <br />
 
 **Verifique se o email foi enviado com sucesso**
 ![alt text](https://github.com/Lmanoel1994/SSIS_Email/blob/master/pictures/7.png) <br />
 
 
