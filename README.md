# Tenda-AIC8800DC
FIXED DRIVER for Tenda U2 AX300
this driver tested on kernel 6.11.5
Linux parrot 6.11+parrot-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.11.5-1parrot1 (2024-12-13) x86_64 GNU/Linux

the problem were in this file U2 Driver for Linux(3.10-6.8)/ax300/usr/src/tenda/aic8800/drivers/aic8800/aic8800_fdrv/rwnx_main.c
the correct way to call cfg80211_ch_switch_notify() is with three arguments (link_id was added in 5.19).

The Solution:
#if LINUX_VERSION_CODE >= KERNEL_VERSION(5, 19, 0)
    cfg80211_ch_switch_notify(vif->ndev, &csa->chandef, 0);  // Kernel ≥5.19 (3 args)
#else
    cfg80211_ch_switch_notify(vif->ndev, &csa->chandef);     // Kernel <5.19 (2 args)
#endif

and this  cfg80211_ch_switch_started_notify

thanks to https://github.com/Z0mbl03 for making a video https://youtu.be/pBrbcStK34M?si=4ZmV2LyKDYziiFUz and a fixed version of driver https://github.com/Z0mbl03/Tenda_AIC8800DC
but it didnt work for me try his driver if mine didnt work 
