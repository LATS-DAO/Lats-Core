Lats Core repository
=====================================

### Coin Specs

$Lats coin (PivX fork) is a layer 1 cryptocurrency. The meaning of "Lats" = it is the name of the national currency that Latvia gave away after joining the economic alliance of the EU (good or bad > not for us to decide).

<h2>Coin Specs</h2>
<ul>
  <li>Name: Lats</li>
  <li>Ticker: LATS</li>
  <li>Proof of Stake (PoS) Algorithm: QUARK</li>
  <li>Total Supply: Unlimited</li>
  <li>Premine: 0</li>
  <li>Block Time: 60 Seconds</li>
  <li>Maturity: 20 Confirmations</li>
  <li>MN Collateral: 1000</li>
  <li>Block Time: 60 Seconds</li>
  <li>Maturity: 100 Confirmations</li>
  <li>Addresses start with the capital letter "L"</li>
  <li>Port: 45454</li>
</ul>

<h3>Genesis Block</h3>
<ul>
  <li>Sun, 30 Oct, 2022 07:26:40 PDT</li>
  <li>Block Height: 0</li>
  <li>Link: https://www.coinexplorer.net/LATS/block/0000043c6a01c787536012ecc33959ceadc7a270c6e3de8951b8ade35dc56534</li>
</ul>

<h3> Proof of Work (PoW) Launch Phase</h3>
<ul>
  <li>Block #1: Nov 21, 2022</li>
  <li>PoW Phase: 1-1000 / Mining reward: 100 $Lats</li>
  <li>PoW Phase Algorithm: X11KVS</li>
  <li>Block 1: </li>
  <li>Block 1000: https://explorer.lats.cc/block/0000005d5b2950ba2ed8a37cddc056c2977f88d522851c77bc24335552d8df68</li>
</ul>

<h3>More details on Proof of Stake (PoS) launch stages</h3>
<li>PoS Blocks:</li>
  <ul>
    <li>v1 1001 - 1050 (MN reward = 0)</li>
    <li>v2 1051 - 2000 (MN reward = 0) // ref: https://github.com/LATS-DAO/Lats-Core/blob/main/src/chainparams.cpp</li>
    <li>v3 from 2001 where PoW rewards are split between MN and Stakers: https://github.com/LATS-DAO/Lats-Core/blob/main/src/validation.cpp</li>
  </ul>
<li><li>Block 1001: https://explorer.lats.cc/block/6566da2a064972a9a80fcbe6873d8f015eee2966142a897386367d437ab3815d</li>
</ul>

=========

<h3>Tokenomics:</h3>
<ul>
<li>Premine = 0 (in Genesis) // blocks 1 - 2000 mined privately (after 2 failed “fair & and open” launch attempts) = 200’000 $Lats</li>
    Note: we plan to burn 200’000 $Lats
<li>1st 1000 blocks are PoW, the reward was 100 $Lats/block</li>
<li>1001 - 2000 > PoS (staking + masternodes) the reward was 100 $Lats/block</li>
<li>At block #2001 Start of normal PoS</li>
<li>Maximum Supply: Unlimited</li>
<li>Total Supply: 1’552’412 LATS</li>
<li>Circulation Supply: 1’035’390.95 LATS</li>
<li>Masternode cost: 1000</li>
</ul>

=========

<h3>Block Rewards:</h3>
Ref: https://github.com/LATS-DAO/Lats-Core/blob/main/src/validation.cpp
<ul>
<li>Block 1 to 1000 = 100 $Lats per block (end of the PoW stage)</li>
<li>1001 - 2000 = 100 (High reward PoS stage)</li>
<li>2001 - 192'000 = 9</li>
<li>192'001 - 300'152 = 4.5</li>
<li>300'153 - 800'153 = 2.5</li>
<li>800'154 - 1'600'154 = 1.5</li>
<li>1'600'155 - unlimited = 1</li>
</ul>

=========

<h2>Masternode vs Staker Reward split:</h2>
Ref: https://github.com/LATS-DAO/Lats-Core/blob/main/src/validation.cpp 

<ul>
<li>Block 1 to 1000 (PoW stage 1) = 100 to Miner</li>
<li>1001 - 2'000 (PoS) = 100 to Staker</li>
<li>2001 - 192'000 =  6 $Lats coins to MN & 3 $Lats coins to Staker</li>
<li>192'001 - 300'152 = 40% MN & 60% Staker = 1.8 coins for MN vs 2.7 for Stake</li>
<li>300'153 - 800'153 = 45% MN & 55% Staker = 1.125 vs 1.375</li>
<li>800'154 - 1'600'154 = 50% MN & 50% Staker = 0.75 vs 0.75</li>
<li>1'600'155 - 3'000'155 = 55% MN & 45% Staker = 0.55 vs 0.45</li>
<li>3'000'156 - 9'900'157 = 60% MN & 40% Staker = 0.6 vs 0.4</li>
<li>9'900'158 - 16'400'158 = 65% MN & 35% Staker = 0.65 vs 0.35</li>
<li>16'400'159 - unlimited = 70% MN & 30% Staker = 0.7 vs 0.3</li>
</ul>

The Budget (also known as DAO payments) will be 10% of the block reward, which users can claim for their budgets every 43'200 blocks.
Note: Budget coins are NOT included in a block reward - they come from a Superblock (generated based on approved proposals every 43'200 blocks) with a maximum of 10% of the block rewards.

=========

<h3>Addnodes:</h3>
<ul>
<li>addnode=94.130.95.107</li>
<li>addnode=94.130.95.108</li>
<li>addnode=94.130.95.110</li>
<li>addnode=188.40.233.34</li>
<li>addnode=188.40.233.35</li>
<li>addnode=188.40.233.38</li>
<li>addnode=188.40.233.39</li>
<li>addnode=188.40.233.40</li>
<li>addnode=188.40.233.41</li>
<li>addnode=188.40.233.43</li>
<li>addnode=188.40.233.44</li>
<li>addnode=188.40.233.45</li>
</ul>

==================
==================
<h2>Links</h2>
==================

<h3>Basic Links:</h3>
<ul>
<li>Website: https://www.lats.cc</li>
<li>GitHub: https://github.com/LATS-DAO/Lats-Core</li>
<li>Wallets: https://github.com/LATS-DAO/Lats-Core/releases</li>
<li>Bitcointalk announcement: https://bitcointalk.org/index.php?topic=5420885</li>
<li>Logo: https://i.imgur.com/kvHCt7S.png</li>
<li>Genesis block: https://www.coinexplorer.net/LATS/block/0000043c6a01c787536012ecc33959ceadc7a270c6e3de8951b8ade35dc56534</li>
<li>Block 1: https://explorer.lats.cc/block/0000022d024c3732a9bbfcb862c9e64a85ddc11a046bc6b6efe01e1eb073fd0e</li>
</ul>

=========

<h3>Explorers</h3>
<ul>
  <li>Official Explorer: https://explorer.lats.cc</li>
  <li>CoinExplorer Explorer: https://www.coinexplorer.net/LATS/</li>
</ul>

=========

<h3>Bootstrap</h3>
<ul>
  <li>https://bootstrap.lats.cc/</li>
</ul>

=========

<h3>Communities</h3>
<ul>
  <li>Forum: https://forums.lats.cc</li>
  <li>Discord: https://discord.gg/xVvajam5u2</li>
  <li>Telegram: https://t.me/latscoin</li>
</ul>

=========

<h3>More on Latvia</h3>
<ul>
  <li>Original Lats (Wikipedia): https://en.wikipedia.org/wiki/Latvian_lats</li>
  <li>Latvia (country): https://en.wikipedia.org/wiki/Latvia</li>
</ul>

=========

<h3>Trading Pairs</h3>

<h4>Xeggex:<h4>
<ul>
<li>LATS / BTC: https://xeggex.com/market/LATS_BTC</li>
<li>LATS / LTC: https://xeggex.com/market/LATS_LTC</li>
</ul>

<h4>FreiXLite:<h4>
<ul>
<li>LATS / LTC: https://freixlite.com/market/LATS/LTC</li>
</ul>

<h4>Stakecube (Warning: insolvent exchange):<h4>
<ul>
<li>LATS / BTC: https://stakecube.net/app/exchange/lats_btc</li>
<li>LATS / SCC: https://stakecube.net/app/exchange/lats_scc</li>
</ul>

=========

<h3>Team</h3>
<h4>Founder: Helmuts Meskonis, No Stress Ltd (UK)</h4>
<ul>
  <li>Linkedin: https://www.linkedin.com/in/helmutsmeskonis/</li>
  <li>Github: https://github.com/helmuc</li>
  <li>Twitter: https://twitter.com/helmutsmeskonis</li>
  <li>Telegram: https://t.me/helmutsm</li>
</ul>

<h4>Stage 1 (completed) development: Liquid369 (USA)</h4>
<ul>
  <li>Github: https://github.com/Liquid369</li>
  <li>Twitter: https://twitter.com/liquid369</li>
</ul>

<h4>Developer and Security Consultant: Christian M. (USA)</h4>
<ul>
  <li>Github: https://github.com/SpectreSecurity</li>
  <li>Linkedin: https://www.linkedin.com/in/christian-marvel-8a910154/</li>
</ul>

<h4>Contractor: Graphics: Felikss Veilands (Republic of Ireland)</h4>
<ul>
  <li>Linkedin: https://www.linkedin.com/in/felikss-veilands/</li>
  <li>Twitter: https://twitter.com/FelikssVeilands</li>
</ul>

<p>.. more information will be added with time..</p>
