# bot
.const Discord = require('discord.js');
const bot = new Discord.Client();
const token = require("./token.json")


bot.on("ready", async () =>{
    console.log("le bot est allumer");
    bot.user.setStatus('dnd');
    setTimeout(() => {
        bot.user.setActivity("dev by Ⱨ₳ⱤØ₱™#0001");
    }, 100)
});

bot.on("guildMemberAdd", member => {
   bot.channels.cache.get ('745366285776584866').send('Bienvenue a toi sur le serveur ${member.user.username}!');
   member.roles.add('745262349841072179')

})



bot.on("message", message => {

    if(message.content.startsWith("!clear")){
    message.delete();
        if(message.member.hasPermission('MANAGE_MESSAGES')){

            let args = message.content.trim().split(/ +/g);

            if(args[1]){
                if(!isNaN(args[1]) && args[1] >= 1 && args[1] <= 99){

                message.channel.bulkDelete(args[1])
                message.channel.send(`Vous avez supprimé ${args[1]} message(s)`)


            }
            else{
                message.channel.send(`Vous devez indiquer une valeur entre 1 et 99 !`)
            }

            }
            else{
                message.channel.send(`Vous devez indiquer un nombre de message a supprimer !`)
            }
        }
        else{
            message.channel.send(`Vous devez avoir la permission de gérer les message pour executer cette commande !`)
        }
    }
    
    if (message.content.startsWith('!kick')) {
        
        const user = message.mentions.users.first();
        
        if (user) {
          
          const member = message.guild.member(user);
          
          if (member) {
            
            
             
            member
              .kick('Optional reason that will display in the audit logs')
              .then(() => {
                
                message.reply(`Successfully kicked ${user.tag}`);
              })
              .catch(err => {
                
                message.reply('I was unable to kick the member');
                
                console.error(err);
              });
          } else {
            
            message.reply("That user isn't in this guild!");
          }
          
        } else {
          message.reply("You didn't mention the user to kick!");
        }
      }
      client.on('ready', () => {
        console.log('I am ready!');
      });
      
      client.on('message', message => {
        
        if (!message.guild) return;
      
        
        if (message.content.startsWith('!ban')) {
         
          
          const user = message.mentions.users.first();
          
          if (user) {
            
            const member = message.guild.member(user);
            
            if (member) {
              
              member
                .ban({
                  reason: 'They were bad!',
                })
                .then(() => {
                  
                  message.reply(`Successfully banned ${user.tag}`);
                })
                .catch(err => {
                  
                  message.reply('I was unable to ban the member');
                  
                  console.error(err);
                });
            } else {
              
              message.reply("That user isn't in this guild!");
            }
          } else {
            
            message.reply("You didn't mention the user to ban!");
          }
        }
      });
});
  

    
    
    
bot.login(token.token);
