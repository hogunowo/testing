publishing all code i need here



layourt of command handler

const Discord = require('discord.js');
const { ask, colors, bot, getMs, errorEmbed } = require('../util/functions')
const fs = require('fs');
const config = require('../util/config')


module.exports = {
    name: "help",
    aliases: ['helpme'],
    description: 'Shows an embed like this one.',
    perms: 'NONE',
    run: async (message, args, client) => {
        const embed = new Discord.MessageEmbed().setColor(colors.green).setAuthor(`${bot.name} - Help`, message.author.displayAvatarURL()).setTimestamp().setDescription(`Here are all the bot commands! My prefix in this server is \`${config.prefix}\`\n`);
        var allCmds = fs.readdirSync(`./commands/`).filter(c => c.endsWith(".js")).sort();
        allCmds.forEach(cmd => {
            var command = require(`../commands/${cmd}`);
            embed.setDescription(embed.description + `\n\`${config.prefix}${command.name}\` • ${command.description}`)

        })
        message.channel.send(embed)

    }
}
