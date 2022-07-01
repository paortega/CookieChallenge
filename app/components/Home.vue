<template>
    <Page>
        <ActionBar title="Home" />
        <ScrollView>
            <StackLayout class="home-panel">
                <Label v-if="!game" textWrap="true" text="Create new player"
                    class="h2 description-label" />
                <TextField v-if="!game" v-model="textFieldValue"
                    class="text-label" placeholder="Name" hint="Name*" />
                <Label v-if="loginFailed" textWrap=" true"
                    text="Name required" class="h4 description-label-error" />
                <Button v-if="!game" text="JOIN" class="btn-app"
                    @tap="onButtonTap" />

                <Button v-if="game" text="LOG OUT" class="btn-logout"
                    @tap="onButtonLogout" />
                <TextView v-if="game" editable="false">
                    <FormattedString>
                        <Span class="h2 description-label" text="Hi " />
                        <Span class="h2 description-label"
                            :text="textFieldValue" />
                    </FormattedString>
                </TextView>
                <TextView v-if="game" editable="false">
                    <FormattedString>
                        <Span class="h2 description-label"
                            text="Merged pull requests: " />
                        <Span class="h2 description-label" :text="count" />
                    </FormattedString>
                </TextView>
                <TextView v-if="autoMerges" class="auto-merge"
                    editable="false">
                    <FormattedString>
                        <Span class="h2 description-label"
                            text="Auto merges: " />
                        <Span class="h2 description-label"
                            :text="countMerges" />
                    </FormattedString>
                </TextView>
                <Button v-if="game" text="MERGE" class="btn-app"
                    @tap="onButtonMerge" />
                <Button v-if="autoBtn" text="BUY AUTO MERGER (50)"
                    class="btn-app" @tap="onButtonBuyMerge" />
            </StackLayout>
        </ScrollView>
    </Page>
</template>

<script>
    export default {
        methods: {
            onButtonTap() {
                if (this.textFieldValue == "") this.loginFailed = true;
                else {
                    this.loginFailed = false;
                    this.game = true;
                }
            },
            onButtonMerge() {
                if (this.autoClickerBaseCost > 0) {
                    this.count++;
                    this.autoClickerBaseCost--;
                } else {
                    this.autoBtn = true;
                    this.autoMerges = true;
                }
            },
            onButtonBuyMerge() {
                this.autoClickerBaseCost = this.autoClickerBaseCost + 50;
                this.autoBtn = false;
                this.countMerges++;
            },
            onButtonLogout() {
                this.game = false;
                this.textFieldValue == "";
            }
        },

        data() {
            return {
                textFieldValue: "",
                count: 0,
                autoClickerBaseCost: 50,
                autoBtn: false,
                loginFailed: false,
                game: false,
                countMerges: 0,
                autoMerges: false
            };
        }
    };
</script>

<style scoped>
    * {
        background: #000;
    }

    .home-panel {
        vertical-align: center;
        font-size: 20;
        margin: 15;
    }

    .description-label {
        margin-bottom: 15;
        color: #FFF;
    }

    .text-label {
        color: #FFF;
    }

    .description-label-error {
        color: red;
    }

    .btn-logout {
        width: 25%;
    }

    .auto-merge {
        margin-top: -200px;
    }
</style>