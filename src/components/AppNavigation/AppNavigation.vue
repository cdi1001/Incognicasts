<template>
  <div>
    <div :style="styles.wrapper">
      <p :style="styles.title" class="stormhacks__title">
        The UI Kit has different ways to make fully customizable UI required to
        build a chat application.
      </p>
      <p :style="styles.subTitle" class="stormhacks__subtitle">
        The UI Kit has been developed to help developers of different levels of
        experience to build a chat application in a few minutes to a couple of
        hours.
      </p>

      <div
        :key="i"
        :style="styles.component"
        class="stormhacks__component"
        v-for="(type, i) in Object.keys(components)"
      >
        <div
          :key="i"
          :style="styles.box"
          class="stormhacks__box"
          v-for="({ title, image, desc, href }, i) in components[type]"
        >
          <div :style="styles.titleWrapper">
            <div :style="styles.thumbnailWrapper">
              <comet-chat-avatar
                border-width="0px"
                :image="`images/${image}.png`"
              />
            </div>
            <h2 :style="styles.componentTitle">{{ title }}</h2>
          </div>
          <div :style="styles.descWrapper">
            <p v-html="desc"></p>
          </div>
          <ul :style="styles.linkWrapper" class="stormhacks__link__wrapper">
            <li>
              <a class="stormhacks__link" :style="styles.link" :href="href">
                Launch
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>

    <div :style="styles.logoutBtn">
      <button @click="logout" :style="styles.logoutBtn.button">Logout</button>
    </div>
    <div :style="{ height: '32px' }"></div>
  </div>
</template>

<script>
import { CometChat } from "@cometchat-pro/chat";
import { CometChatAvatar } from "../../cometchat-pro-vue-chat-ui-kit/";

import * as style from "./style";

export default {
  name: "AppNavigation",
  components: { CometChatAvatar },
  data() {
    return {
      components: {
        chatComponents: [
          {
            title: "CometChatUI",
            href: "#/embedded-app",
            image: "rocket",
            desc:
              "The <code>CometChatUI</code> component launches a fully working chat application.",
          },
        ],
        screenComponents: [
          {
            title: "Conversations",
            href: "#/conversation-screen",
            image: "components",
            desc:
              "The <code>CometChatConversationListWithMessages</code> component launches Conversation list with messaging.",
          },
          {
            title: "Groups",
            href: "#/group-screen",
            image: "components",
            desc:
              "The <code>CometChatGroupListWithMessages</code> component launches Group list with messaging.",
          },
          {
            title: "Users",
            href: "#/user-screen",
            image: "components",
            desc:
              "The <code>CometChatUserListWithMessages</code> component launches User list with messaging.",
          },
        ],
        listComponents: [
          {
            title: "Conversation List",
            href: "#/conversation-list",
            image: "bricks",
            desc:
              "The <code>CometChatConversationList</code> component launches Conversation list.",
          },
          {
            title: "Group List",
            href: "#/group-list",
            image: "bricks",
            desc:
              "The <code>CometChatGroupList</code> component launches Group list.",
          },
          {
            title: "User List",
            href: "#/user-list",
            image: "bricks",
            desc:
              "The <code>CometChatUserList</code> component launches User list.",
          },
        ],
      },
    };
  },
  created() {
    CometChat.getLoggedinUser().then(
      (user) => {
        console.log("we are here", user);
        if (!user) {
          location.href = "/";
        }
      },
      (error) => {
        console.log(error);
        location.href = "/";
      }
    );
  },
  computed: {
    styles() {
      return {
        wrapper: style.wrapperStyle(),
        title: style.titleStyle(),
        subTitle: style.subTitleStyle(),
        helpText: style.helpTextStyle(),
        component: style.componentStyle(),
        box: style.boxStyle(),
        titleWrapper: style.titleWrapperStyle(),
        thumbnailWrapper: style.thumbnailWrapperStyle(),
        componentTitle: style.componentTitleStyle(),
        descWrapper: style.descWrapperStyle(),
        linkWrapper: style.linkWrapperStyle(),
        link: style.linkStyle(),
        logoutBtn: style.logoutBtn(),
      };
    },
  },
  methods: {
    logout() {
      CometChat.logout().then(() => {
        location.href = "/";
      });
    },
  },
};
</script>
<style>
code {
  padding: 2px;
  font-size: 105%;
  color: crimson;
  border-radius: 4px;
  background-color: #f1f1f1;
}
</style>

<style scoped>
li {
  list-style-type: none;
}
.stormhacks__link {
  color: darken(rgb(67, 171, 255), 20%);
  font-weight: 600;
  font-size: 14px;
}
@media (min-width: 320px) and (max-width: 767px) {
  .stormhacks__title {
    font-size: 20px;
  }
  .stormhacks__subtitle {
    font-size: 16px;
  }
  .stormhacks__box {
    width: 400px;
  }
  .stormhacks__link__wrapper {
    flex-direction: column;
  }
  .stormhacks__link__wrapper li {
    padding: 10px;
  }
  .stormhacks__component {
    flex-direction: column;
    padding: 50px 100px;
  }
}
@media (min-width: 768px) and (max-width: 1024px) {
  .stormhacks__component {
    flex-direction: column;
    padding: 50px 50px;
  }
}
</style>