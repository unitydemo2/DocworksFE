Game Saves
======

Unity provides ``UnityEngine.WiiU.Save`` and ``UnityEngine.WiiU.SaveCommand`` classes to query free space available and to work with file system journaling.

It is important to call ``SaveCommand.FlushQuota`` after writing all game-save related files, otherwise they will disappear after the system is rebooted. Make sure you test saving features when writing to NAND memory, because only for that flushing quota is relevant. PCFS saving won't exhibit these issues.

This is an example for saving data:

````
using UnityEngine;
using System.IO;
using WiiU = UnityEngine.WiiU;

public class SaveGameState : MonoBehaviour
{
    public bool DoSave()
    {
        WiiU.SaveCommand cmd = WiiU.Save.SaveCommand(WiiU.Save.accountNo);

        long freespace = 0;
        WiiU.Save.FSStatus status = cmd.GetFreeSpaceSize(out freespace, WiiU.Save.FSRetFlag.None);
        if (status != WiiU.Save.FSStatus.OK)
            return false;

        long needspace = Mathf.Max(1024 * 1024, WiiU.PlayerPrefsHelper.rawData.Length);

        if (freespace < needspace)
        {
            // not enough free space
            return false;
        }
        else
        {
            var path = Application.persistentDataPath + "/mysave1.bin";
            var fileStream = new FileStream(path, FileMode.Create);
            byte[] prefsData = WiiU.PlayerPrefsHelper.rawData;
            fileStream.Write(prefsData, 0, prefsData.Length);
            fileStream.Close();

            // It is very important to flush quota, otherwise filesystem changes will be discarded upon reboot
            status = cmd.FlushQuota(WiiU.Save.FSRetFlag.None);
            if (status != WiiU.Save.FSStatus.OK)
                return false;
        }

        return true;
   }
}
````
