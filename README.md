CS185C-Bukkit-AdvancedChat-Plugin
=================================
import java.util.logging.Logger;

import org.bukkit.plugin.java.JavaPlugin;

import org.apache.commons.lang.StringUtils;
import org.bukkit.ChatColor;
import org.bukkit.command.Command;
import org.bukkit.command.CommandSender;
import org.bukkit.entity.Player;
import org.bukkit.plugin.PluginDescriptionFile;

 
public final class hello extends JavaPlugin {
    public final Logger logger = Logger.getLogger("Minecraft");
    public static hello plugin;
 
    @Override
        public void onEnable(){
        PluginDescriptionFile pdffile = this .getDescription();
        this.logger.info(pdffile.getName() + " Has been enabled!");
    }
    
    @Override
        public void onDisable(){
        PluginDescriptionFile pdffile = this .getDescription();
        this.logger.info(pdffile.getName() + " Has been disabled!");
    }
 
    public boolean onCommand(CommandSender sender, Command cmd, String commandLabel, String[] args){
        Player s = (Player)sender;
 
        if((commandLabel.equalsIgnoreCase("im"))){ //  Instant messaging system activate
            if(args.length == 0){
                s.sendMessage(ChatColor.DARK_RED + "Incorrect Usage! Correct Usage: /im (player) (message)");
            }
            else if(args.length == 1){
                s.sendMessage(ChatColor.DARK_RED + "Incorrect Usage! Correct Usage: /im (player) (message)");
            }
            else if(args.length > 1){ // Anything after the players name will be sent to the target
                Player target = s.getServer().getPlayer(args[0]); // Get target players name
                s.sendMessage(ChatColor.GREEN + "Message Sent");
                target.sendMessage(ChatColor.BLUE + "Received private message from " + sender.getName() + ":");
                target.sendMessage(ChatColor.GREEN + StringUtils.join(args, ' ', 1, args.length)); // Send message to target player
            }
        }
        if(cmd.getName().equalsIgnoreCase("imstart")){ // Chat room between 2 players system
            if(args.length == 0){
                s.sendMessage(ChatColor.DARK_RED + "Incorrect Usage! Correct Usage: /imstart (player)");
            }
            else if(args.length == 1){
                Player target = s.getServer().getPlayer(args[0]);
                // Start of chat room
 
                s.sendMessage(ChatColor.GREEN + "You are now in a chat with" + target.getName());
                target.sendMessage(ChatColor.GREEN + "You are now in a chat with" + s.getName());
                s.sendMessage(ChatColor.GREEN + "All other chat will be blocked out. Use /imstop to stop the chat.");
                target.sendMessage(ChatColor.GREEN + "All other chat will be blocked out. Use /imstop to stop the chat.");
            } else if(args.length > 1){
                s.sendMessage(ChatColor.DARK_RED + "Incorrect Usage! Too many arguments! Correct Usage: /imstart (player)");
            }
        }
        if(cmd.getName().equalsIgnoreCase("imstop")){
            if(args.length == 0){
                // End chat room session
 
                s.sendMessage(ChatColor.RED + "Chat Ended");
            }
            if(args.length > 0){
                s.sendMessage(ChatColor.DARK_RED + "Incorrect Usage! Too many arguments! Correct usage: /imstop");
            }
        }
        if(cmd.getName().equalsIgnoreCase("imblock")){
            if(args.length == 0){
                s.sendMessage(ChatColor.RED + "Incorrect Usage. Correct Usage: /imblock (playername)");
            }
            if(args.length == 1){
                Player target = s.getServer().getPlayer(args[0]);
                target.sendMessage(ChatColor.RED + sender.getName() + " has blocked you!");
                s.sendMessage(ChatColor.RED + "Blocked user" + target.getName());
            }
            if(args.length > 1){
                s.sendMessage(ChatColor.DARK_RED + "Incorrect Usage! Too many arguments! Correct Usage: /imblock (username)");
            }
        }
 
        return false;
    }
 
}
 
