---
emoji: 🎮 
title: How to set up ios target using Unity resolver
date: '2024-07-14 15:20:00'
author: Derrick
tags: Unity Unityresolver
categories: Unity
---

Currenlty I am using some iOS Native Sdks using Unity resolver and Cocopods
There were one requeiments after build from unity edtor , it should set antoher iOS target not app's target

Firebase and Adsmob's native sdk modules are composed by Unity Resolver

The module's target can be found in the API below, as shown in the unity resolver guide. 
However, the order must be  It should be between 40 and 50

    using System.IO;

    using UnityEditor;
    using UnityEditor.Callbacks;
    using UnityEngine;

    public class PostProcessIOS : MonoBehaviour
    {
        // Must be between 40 and 50 to ensure that it's not overriden by Podfile generation (40) and
        // that it's added before "pod install" (50).
        [PostProcessBuildAttribute(45)]
        private static void PostProcessBuild_iOS(BuildTarget target, string buildPath)
        {
            if (target == BuildTarget.iOS)
            {
                using (StreamWriter sw = File.AppendText(buildPath + "/Podfile"))
                {
                    // E.g. add an app extension
                    sw.WriteLine("\ntarget 'NSExtension' do\n  pod 'Firebase/Messaging', '6.6.0'\nend");
                }
            }
        }
    }

 
https://github.com/googlesamples/unity-jar-resolver
