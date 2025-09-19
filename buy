embed <drac2>
using(baglib="5f1ffcbf-3f59-4396-b402-1ca0f02d6bbb")
args = &ARGS&
ch = character()
bagsLoaded = baglib.LoadedBags()
autoCoins = baglib.settings.get('autoCoins',get("autocoins","0")=="1")
compact = baglib.settings.get('compactCoins',get("compactcoins","0")=="1")
openMode = baglib.settings.get('openMode','all').lower()
item = " ".join(args[:-1]) if len(args) > 1 else None
coin_str = args[-1] if args else ""
delta, coin_error = baglib.parsecoins(coin_str)
focus = None
bagsLoaded['error'] |= coin_error
cmd = ctx.prefix + ctx.alias
title = f""
text = f"## [GALACTIC TRADE NETWORK](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRtr9qQamwZTQWTQzZI4m6aG_ScDAjpxPRyaQ-6HnmDYxDPFej7hk2QctU&s=10)"
text += f"\n\n**[==============================]**\n**|\u00A0\u00A0GALACTIC\u00A0\u00A0TRADE\u00A0\u00A0NETWORK\u00A0\u00A0\u00A0|**\n**|\u00A0\u00A0Access\u00A0Level:\u00A0PUBLIC\u00A0MARKET\u00A0\u00A0|**\n**[==============================]**"
positive = False
if delta:
    focus = bagsLoaded.modify_coins(autoCoins=autoCoins, delta = delta)
    if not bagsLoaded.error:
        delta = list(delta.items())
        delta.sort(key=lambda x: x[1], reverse=True)
        if delta[0][1]>0:
            display = f"Selling Listing:\n...Loading...\nItem:{item}{name} is selling a... {item}"
            positive = True
if not bagsLoaded.error:
    for idx, cointup in enumerate(delta):
        coin, quantity = cointup
        display += f"{'' if idx == 0 else ',' if (positive and quantity>0) or (not positive and quantity<0) else ', and removes'} {baglib.round_nicely(abs(quantity))} {coin}"
        if positive and quantity<0:
            positive = False
bag_name = "Coin Purse" if bagsLoaded.use_coin_purse() else baglib.coinPouchName
if delta:
    display = f" to their {bag_name}" if positive else f" from their {bag_name}"
else:
    display = f" their {bag_name}"
if not focus:
    bagsLoaded.get_coins()
if bagsLoaded.internal_bag_data:
    success = bagsLoaded.save_bags()
else:
    success = -1 if bagsLoaded.error else 1
if coin_error:
    text = ""
    display = '-f ＂`&*&` contained invalid coins＂'
elif openMode != 'none':
    title = f" "
    display = ' '.join(bagsLoaded.display_coins(compact))
    text += f"\n\n**Selling Listing:**"
    text += f"\n*...Loading...*"
    text += f"\n\n**Item: {item}**"
    text += f"\n{name} is selling a... {item}"
    text += f"\n\n**Price: {quantity}**"
    text += f"\n...For {quantity} credits!"
    text += f"\n\n**Seller name: {name}**"
    text += f"\nSelling...Authorization, Complete!"
    text += f"\n\n**TRANSACTION COMPLETED!**"
    text += f"\nCredits are been credited to your account. Please cross check, the Galactic Trade Center does not take any responsibility of any theft from this point onwards."
    text += f"\n\n**[=============================]**"
    text += f"\n**|\u00A0\u00A0\u00A0\u00A0\u00A0END\u00A0\u00A0\u00A0\u00A0OF\u00A0\u00A0\u00A0TRANSMISSION\u00A0\u00A0\u00A0\u00A0\u00A0|**"
    text += f"\n**[=============================]**"
else:
    text = ""
    display = ""
title = [f"{name} tries to add to their {bag_name} but can't find it.", title, f"{name} can't afford that much."][success]
return f"""-title "{title}" -desc "{text}" {display} -color #5197ed """
</drac2>
-footer ＂{{get('coinFooter') or get_svar('coinFooter', f"View '{ctx.prefix}help {ctx.alias}' for more help")}}＂
-thumb ＂https://imgur.com/CxFqWoH.png＂
