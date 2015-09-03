### Issue for diaspora > tumblr

https://github.com/diaspora/diaspora/issues/5397

### Tumblr API documentation

https://www.tumblr.com/docs/en/api/v2

### Ruby Gem for tumblr (not yet used in Diaspora)

https://github.com/tumblr/tumblr_client/tree/master/lib/tumblr

### What we found out

* strange behaviour: if you connect with tumblr your username in diaspora changes (also stays for following sessions)

#### Server log for posting to tumblr
```
Rails: Started POST "/status_messages" for 127.0.0.1 at 2015-09-03 12:18:17 +0200
[2015-09-03T12:18:17] INFO  PID-17600 TID-70197352727040 ActionController::Base: Processing by StatusMessagesController#create as JSON
[2015-09-03T12:18:17] INFO  PID-17600 TID-70197352727040 ActionController::Base:   Parameters: {"status_message"=>"[FILTERED]", "aspect_ids"=>"all_aspects", "services"=>"tumblr", "location_coords"=>"", "poll_question"=>"", "poll_answers"=>["", ""]}
[2015-09-03T12:18:17] DEBUG PID-17600 TID-70197352727040 Rails: ETHON: Libcurl initialized
[2015-09-03T12:18:19] DEBUG PID-17600 TID-70197352727040 Rails: ETHON: performed EASY effective_url=http://asset-1.soupcdn.com/asset/12918/3824_1822_500.jpeg response_code=200 return_code=ok total_time=1.605934
[2015-09-03T12:18:19] INFO  PID-17600 TID-70197352727040 User: user:1 dispatching StatusMessage:04c13fc0345301332fce48d705df9e7b
[2015-09-03T12:18:21] INFO  PID-17600 TID-70197352727040 Postzord::Receiver::LocalBatch: receiving local batch for #<StatusMessage id: 37, author_id: 1, public: false, diaspora_handle: "test@localhost:3000", guid: "04c13fc0345301332fce48d705df9e7b", pending: false, type: "StatusMessage", text: "Cosmonaut!\r\n![](http://asset-1.soupcdn.com/asset/1...", remote_photo_path: nil, remote_photo_name: nil, random_string: nil, processed_image: nil, created_at: "2015-09-03 10:18:17", updated_at: "2015-09-03 10:18:21", unprocessed_image: nil, object_url: nil, image_url: nil, image_height: nil, image_width: nil, provider_display_name: nil, actor_url: nil, objectId: nil, root_guid: nil, status_message_guid: nil, likes_count: 0, comments_count: 0, o_embed_cache_id: nil, reshares_count: 0, interacted_at: "2015-09-03 10:18:17", frame_name: nil, facebook_id: nil, tweet_id: nil, open_graph_cache_id: nil, tumblr_ids: "{\"unitedbyphone.tumblr.com\":128252348031,\"fuehl.tu...">
[2015-09-03T12:18:21] INFO  PID-17600 TID-70197352727040 Postzord::Receiver::LocalBatch: receiving local batch completed for #<StatusMessage id: 37, author_id: 1, public: false, diaspora_handle: "test@localhost:3000", guid: "04c13fc0345301332fce48d705df9e7b", pending: false, type: "StatusMessage", text: "Cosmonaut!\r\n![](http://asset-1.soupcdn.com/asset/1...", remote_photo_path: nil, remote_photo_name: nil, random_string: nil, processed_image: nil, created_at: "2015-09-03 10:18:17", updated_at: "2015-09-03 10:18:21", unprocessed_image: nil, object_url: nil, image_url: nil, image_height: nil, image_width: nil, provider_display_name: nil, actor_url: nil, objectId: nil, root_guid: nil, status_message_guid: nil, likes_count: 0, comments_count: 0, o_embed_cache_id: nil, reshares_count: 0, interacted_at: "2015-09-03 10:18:17", frame_name: nil, facebook_id: nil, tweet_id: nil, open_graph_cache_id: nil, tumblr_ids: "{\"unitedbyphone.tumblr.com\":128252348031,\"fuehl.tu...">
[2015-09-03T12:18:21] INFO  PID-17600 TID-70197352727040 Postzord::Dispatcher::Private: event=push route=local sender=test@localhost:3000 recipients=4 payload_type=StatusMessage
[2015-09-03T12:18:22] INFO  PID-17600 TID-70197352727040 Participation: event=sign_with_key status=complete guid=073448f0345301332fce48d705df9e7b
[2015-09-03T12:18:22] INFO  PID-17600 TID-70197352727040 Participation: event=sign_with_key status=complete guid=073448f0345301332fce48d705df9e7b
[2015-09-03T12:18:22] INFO  PID-17600 TID-70197352727040 Participation::Generator: user:1 dispatching Participation:073448f0345301332fce48d705df9e7b
[2015-09-03T12:18:22] INFO  PID-17600 TID-70197352727040 ActionController::Base: Completed 201 Created in 4199ms (Views: 12.9ms | ActiveRecord: 67.1ms)

```
