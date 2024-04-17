---
description: This is a beginner's guide to mining Scash on Windows.
---

# Mining on Windows

There are two ways to mine Scash on your home computer.

Solo mining

* If you mine a block, the entire block reward is yours
* This guide will show how to mine using the GUI wallet app connected to the dedicated CPU mining software cpuminer-scash.

Pooled mining

* You mine with other miners at a pool, and share the block reward with other miners
* This guide will show how to create an address in the GUI wallet app, which you can then use with mining pools.



**Step 1. Download Scash**

Download the latest Scash release from Github: [https://github.com/scash-project/scash/releases/](https://github.com/scash-project/scash/releases/)

You can download either the setup.exe or zip file (which you manually unzip).

{% hint style="info" %}
If Windows Defender complains that the downloaded file is not from a known publisher, click away the warning and continue. Note that it is highly recommended that you verify the downloaded file before running.
{% endhint %}



**Step 2. Verify downloads (optional, highly recommended!)**

For security and to ensure the integrity of the downloaded file, open a Windows Terminal (Powershell) and run the following command to verify the hash of the downloaded file matches the hash shown on the Github release page.

```
 Get-FileHash Downloads\scash-REST-OF-FILENAME
```


**Step 3. Run the installer**

Run the scash windows setup executable. This is a standard Windows installer. Follow the instructions.

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

After running the installer, you can see where the software has been installed using Windows Terminal (Powershell)&#x20;

The default location for the application software is `C:\Program Files\Scash`

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

For reference,

* The file `scash-qt.exe` is the GUI application which you typically launch from the Start menu.

And in the folder `daemon`&#x20;

* the Server application`scashd.exe` (this is the same scash application as the GUI appliction, but without the GUI).
* The tool `scash-cli.exe` which is used to communicate with both the GUI and the server application (whichever one is running).



**Step 4. Launch Scash**

Launch Scash from `Start menu > Program Files > Scash`

Make sure you select Scash for the main network, and not Scash (testnet) which is a testing network.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Note: By default, after launching the Scash application, a user folder called `C:\Users\USERNAME\AppData\Roaming\Scash` will be created as the data directory. This folder is used to store your configuration, your wallet, blockchain data, etc.

{% hint style="info" %}
Windows Explorer does not show the AppData folder. It is a hidden folder. You can change the Windows Explorer settings to show hidden folders.
{% endhint %}



**Step 5. Sync to the network**

After launching the Scash application, it will need to sync up with the main network. This might take a few minutes or longer depending on the network and your connectivity.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

You can click 'Hide' and proceed to create a wallet.

When fully synced, you will see a check mark in the bottom right of the status bar. If you move you mouse over the check mark a tool tip will appear showing some details.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

**Step 6. Create a wallet**

Select the menu option `File > Create Wallet...` to create a wallet. Enter a name and click create.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>



**Step 7. Create an address in your wallet**

Click the Receive tab and create an address where you want to receive your mined coins.  Choose a label for the address which is used in your wallet's address book. Leave the amount and message fields empty.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

After clicking 'Create new receiving address' you should see a new address has been created.  Keep a copy of the address as you will use this with the mining software later.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

If you select the menu option `Window > Receiving addresses` you should see your address there.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

**Mining Pools**

{% hint style="info" %}
As of April 2024 there are mining pools available to mine Scash. Mining pools let miners combine their CPU mining power together and share any coins the pool finds.

The first mining pool for Scash is from Rplant [https://pool.rplant.xyz/#satoshicash#connect](https://pool.rplant.xyz/#satoshicash#connect). It requires special mining software to download and configure. Instructions available at their site.

Note:

1. Scash developers do not endorse or support any mining pools. Users should exercise caution when using mining pool services and software.
2. The cpuminer-scash can only be used for solo mining. Support for connecting to mining pools will be added soon.
{% endhint %}

**Step 8. Edit configuration file**

Now you need to configure the Scash application so that the mining software can communicate with it.

Selec the menu item `Settings > Options` and then:

* Select `Enable RPC server`
* Click `Open Configuration File`.

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

This will open the `scash.conf` configuration file in the data directory shown earlier. The file may be empty. Add the following to the file:

```
rpcuser=aladdin
rpcpassword=opensesame
```

This is the username and password which tools like the mining software will use when communicating with Scash. Without this, the mining software will not be able to connect to Scash.

There is an advanced setting called `randomxfastmode` which is not required because you are using dedicated cpu mining software to mine, instead of the Scash application itself.

* Miners running the Scashd node with large amounts of memory can enable this option to improve block verification time. The cpuminer already runs in this mode. See spec here for more details: [https://github.com/scash-project/sips/blob/main/scash-protocol-spec.md#4-algorithm-performance](https://github.com/scash-project/sips/blob/main/scash-protocol-spec.md#4-algorithm-performance)

After editing, save and close the document.

**Step 9. Relaunch Scash**

Close Scash and relaunch the application so that it uses the new configuration options. You can relaunch Scash from the Windows start menu as before.

_Optional: Launch Scash without the GUI_

You can also launch Scash as a server application, without the GUI, from the Windows Terminal (Powershell).

&#x20;`C:\Program Files\Scash\daemon\scashd.exe -server`&#x20;

You should see output in the terminal window when the server launches.

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

**Step 10 Test Scash is accepting RPC commands**

Enter the following command in a Windows Terminal (Powershell) to test that Scash is running in server mode and is accepting commands from tools, such as the standard `scash-cli` tool (and later, mining software).

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

You should see output in the terminal similar to above.

If you don't, there is a problem communicating with the server application. Please check the previous steps above before continuing.





**Step 11 Install the CPU mining software**

Scash will now be ready for the mining software to connect to it.

The cpuminer-scash mining software runs in MSYS2 for Windows.

1. Download and run installer (https://www.msys2.org/)
2. Launch the MSYS2 terminal. You should see 'UCRT64' in the terminal prompt. You must use MSYS2 in the UCRT64 environment. If not, close and check Start Menu.

Next, it is highly recommended you build the mining software from source: [https://github.com/scash-project/cpuminer-scash?tab=readme-ov-file#windows](https://github.com/scash-project/cpuminer-scash?tab=readme-ov-file#windows)

If you don't want to build from source, copy the URL of the latest binary release from  [https://github.com/scash-project/cpuminer-scash/releases](https://github.com/scash-project/cpuminer-scash/releases), and in MSYS2 terminal:

```
pacman -S mingw-w64-ucrt-x86_64-curl
wget RELEASE_FILE_URL
tar xvf FILENAME
sha256sum minerd.exe
./minerd.exe -h
```





**Step 12 Run the CPU mining software**

Launch MSYS2 (not Windows Terminal) which you installed as part of building the mining software. Run the mining software from the command-line.

This example will connect to the Scash application on your computer and launch 2 mining threads.

`./minerd.exe --url=127.0.0.1:8342 --userpass=aladdin:opensesame --threads=2 --coinbase-addr=YOUR_SCASH_ADDRESS`

The mining software will use just over 2GB of memory.

The username and password must match what you entered in the Scash configuration file from the earlier step.

When mining is running without error, you should see similar output to below:

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

The mining software will run continuously. To stop it, press CTRL-C.



_Performance Tips_

Check your Windows settings:

* Turn off sleep and suspend so Windows doesn't goto sleep when you leave the computer to mine unattended e.g. overnight
* Check your Windows performance profile. The default settings may throttle CPU usage and reduce your mining performance. Example:  [_https://www.howtogeek.com/368781/how-to-enable-ultimate-performance-power-plan-in-windows-10/_](https://www.howtogeek.com/368781/how-to-enable-ultimate-performance-power-plan-in-windows-10/)
* Check any performance settings from computer manufacturer installed management software e.g. from Lenovo, HP, Dell, Asus etc.
* Check performance related settings in your BIOS
* In Windows Task Manager. Select Performance, CPU and right-click over the CPU graph and select Logical Processors to get a detailed view of CPU usage. When mining you should see many of the processors max out.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>



_Help and debugging:_

Run `minerd.exe -h` to see the help file detailing options.

If you run into problems, add the following options when running `minerd`

The option `--debug` will output a lot of detailed diagnostic data.

The option `--protocol-dump` you can verify that the mining software is communicating successfully with Scash, shown below:

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>



_Common Problem: 401 Unauthorized_

Check that the username and password matches what is in the scash.conf configuration file. If they were changed recently, restart Scash to make sure it detects the change.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

_Common Problem: No connection_

Check that the username and password matches what is in the scash.conf configuration file.

Check that the Scash GUI application has the 'Enable RPC server' setting in options is enabled.

Check that the Scash server application `scashd.exe` was launched with the `-server` option.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

_Common Problem: Many longpoll messages every second_

The option `--no-longpoll` can be used if you see a lot of messages appearing on screen `LONGPOLL pushed new work`. This can heppen when Scash has just connected to the network and is not in sync, or has not received a new block in a while. Once new blocks have been found, you can stop the miner and relaunch without this option (for best mining performance, you don't want to run with this option).

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>



**Step 13: Check your Scash mining balance**

You can see any mined coins in the Scash GUI app. They appear with the mining icon in recent transactions.

Also in the MSYS2 window where you launched the mining software, you may see the message `accepted (4/5)`. This means you mined 5 blocks, 1 block was rejected by the network, 4 blocks were accepted. The current block reward is 50 coins, so you would expect to see 50 \* 4 = 200 coins appear in your wallet.

Note that after mining, the coins cannot be spent, they are immature.  It takes another 100 blocks from the time (block) of mining, before they can be spent.

In the example below, a block was mined containing 50 coins, but it is not available for spending yet and is still immature. If the block was mined at block 1000, it can be spent once the network reaches block 1100.

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

