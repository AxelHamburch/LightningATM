## Instruction for testing the LNbits interface 📜🧐

### 1. Update to the new version

Logon via SSH and stop the LightningATM service, make a backup from directory LightningATM clone the new Github to "temp", sync once from "temp" to "LightningAMT" and then delete the "temp" directory that is no longer needed.

    $ sudo systemctl stop LightningATM.service
    $ cp -r -v LightningATM LightningATM_Backup
    $ git clone --branch lnbits-compatibility https://github.com/21isenough/LightningATM.git temp
    $ rsync -a -v temp/ LightningATM/
    $ sudo rm -r temp
    
### 2. Edit config.ini

    $ nano ~/.lightningATM/config.ini

#### 2.1 Add the following

    [lnbits]
    # api credentials
    url = https://legend.lnbits.com/api/v1
    apikey = 

`Note:` User your apikey (API Info / Admin key) from legend.lnbits.com wallet with funding 

#### 2.2 Change active wallet to lnbits

    activewallet = lnbits
    
`CTRL+x` -> `y` -> `Enter`
   
### 3. Start and test the version

    $ cd LightningATM
    $ ./app.py

- It takes a few seconds for the display to update, but then..
- The ATM has started and you can use it normally or test the functions.
- Stop the ATM with `CTRL+C`
- If something went wrong or you just want to watch the ATM, launch a second terminal window, login via ssh and call the debugger: `$ tail -f ~/.lightningATM/debug.log`
- If you like this version? Just keep it and delete the Backup: `$ cd` and then `$ sudo rm -r LightningATM_Backup`

### 4. If you don't like this version and want to get rid of it 

Make the backup the major version again and then delete the backup.

    $ cd
    $ rsync -a LightningATM_Backup/ LightningATM/
    $ sudo rm -r LightningATM_Backup

- Everthing should now be as befor. Even the wallat data.
- You can clean up the coinfig.ini, but you don't have to.

### 5. Final step

Restart the LightningATM service

    $ sudo systemctl start LightningATM.service

- Your ATM should now restart as usual

## Thank you for your patience! ❤
