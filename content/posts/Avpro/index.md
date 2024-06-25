---
emoji: 🎮 
title: Unity AVpro HLS Streaming playback with some events
date: '2024-06-25 15:20:00'
author: Derrick
tags: Unity Avpro
categories: Unity
---

I make an app using unity to support HLS Streaming Playback with Avpro plugin in company


It was very useful and avpro provided good events to make some UI features

E.g

Callback called when seek operation is start or finish


    _mediaPlayer.Events.AddListener(HandleEvent);
    void HandleEvent(MediaPlayer mp, MediaPlayerEvent.EventType eventType, ErrorCode code)
            {
                Debug.Log("[SongPlayer] MediaPlayer " + mp.name + " generated event: " + eventType.ToString());
                if (eventType == MediaPlayerEvent.EventType.Error)
                {
                    PopupManager.Instance.LoadPopup(!SSMembershipUtils.IsEnableInternet()
                        ? CommonConstant.PopupNetwork
                        : CommonConstant.PopupError); // 에러 팝업
                    
                    Debug.LogError("SongPlayer MediaPlayer Error: " + code);
                }
                else if (eventType == MediaPlayerEvent.EventType.FinishedSeeking)
                {
                    _isHoveringOverTimeline = false;
                    Debug.LogError("SongPlayer FinishedSeeking: " + code);
                }
                else if (eventType == MediaPlayerEvent.EventType.StartedSeeking)
                {
                    Debug.LogError("SongPlayer StartedSeeking: " + code);
                }
                else if (eventType == MediaPlayerEvent.EventType.StartedBuffering)
                {
                    Debug.LogError("SongPlayer StartedBuffering: " + code);
                } else if (eventType == MediaPlayerEvent.EventType.FinishedBuffering)
                {
                    Debug.LogError("SongPlayer FinishedBuffering: " + code);
                } else if (eventType == MediaPlayerEvent.EventType.Started)
                {
                    Debug.LogError("SongPlayer  Started: " + code);
                    isPlaying = true;

                    if (isFinished)
                    {
                        _mediaPlayer.Pause();
                        isFinished = false;
                    }

                } else if (eventType == MediaPlayerEvent.EventType.Stalled)
                {
                    if(!SSMembershipUtils.IsEnableInternet()) {
                        PopupManager.Instance.LoadPopup(CommonConstant.PopupNetwork);
                    }

                } else if (eventType == MediaPlayerEvent.EventType.Closing)
                {
                    Debug.LogError(" Closing: " + code);
                } else if (eventType == MediaPlayerEvent.EventType.ReadyToPlay)
                {
                    Debug.LogError(" ReadyToPlay: " + code);
                } else if (eventType == MediaPlayerEvent.EventType.FirstFrameReady)
                {
                    PopupManager.Instance.ReleasePopup();
                    Debug.LogError(" FirstFrameReady: " + code);
                } else if (eventType == MediaPlayerEvent.EventType.FinishedPlaying)
                {
                    Debug.LogError("  MediaPlayerEvent.EventType.FinishedPlaying " + code);

                    ResetUI();
                    
                    var framework = FindObjectOfType<PlayerFramework>();   // 칭찬모션 띄움
                    if(framework) framework.ShowEnding();
                    
                    if(!ActivityNavigator.Instance.IsLearningPath) return;
                    ActivityProgressManager.Instance.SaveStarCount();      // 진척도 저장

                    isFinished = true;
                    
                    Debug.LogError("FinishedPlaying: " + code);
                }      
                
            }
 
In addition, various player-related Event Callback APIs are provided.

https://www.renderheads.com/content/docs/AVProVideo/articles/feature-events.html
