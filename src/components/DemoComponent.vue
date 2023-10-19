<template>
    <div>
        <el-input v-model="postTitle" placeholder="输入帖子标题" style="width: 300px" />
        <el-input v-model="postContent" placeholder="输入帖子内容" style="width: 300px" />
        <el-button @click="addPost">发布帖子</el-button>
        <el-divider></el-divider>
        <el-card v-for="(post, index) in posts" :key="index">
            <p>标题: {{ post.title }}</p>
            <p>内容: {{ post.content }}</p>
            <p>点赞数量: {{ post.likes }}</p> <!-- 显示点赞数量 -->
            <el-divider></el-divider>
            <el-input v-model="comment" placeholder="添加评论" style="width: 200px" />
            <el-button @click="addComment(index)">评论</el-button>
            <el-button @click="likePost(index)">点赞</el-button>
            <el-divider></el-divider>
            <div v-for="(comment, commentIndex) in post.comments" :key="commentIndex">
                {{ comment }}
            </div>

        </el-card>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            postTitle: '',
            postContent: '',
            posts: [],
            comment: '',
        };
    },
    methods: {
        addPost() {
            if (this.postTitle && this.postContent) {
                this.posts.push({
                    title: this.postTitle,
                    content: this.postContent,
                    comments: [],
                    likes: 0,
                });
                this.postTitle = '';
                this.postContent = '';
            }
        },
        addComment(postIndex) {
            if (this.comment) {
                this.posts[postIndex].comments.push(this.comment);
                this.comment = '';
            }
        },
        likePost(postIndex) {
            this.posts[postIndex].likes++; // 增加点赞数量
        },
    },
};
</script>
  