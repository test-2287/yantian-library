<script setup>
import BookCover from '@/assets/svg/book-cover.svg';
import { onMounted } from 'vue';

const monthBookRank = [
    {
        bookName: '思考，好与坏',
        publisher: '重庆出版社',
        author: '杨念群',
        isbn: 9787020184262,
        borrowCount: 62,
        image: ''
    },
    {
        bookName: '思考，好与坏',
        publisher: '重庆出版社',
        author: '杨念群',
        isbn: 9787020184262,
        borrowCount: 62,
        image: ''
    },
    {
        bookName: '思考，好与坏',
        publisher: '重庆出版社',
        author: '杨念群',
        isbn: 9787020184262,
        borrowCount: 62,
        image: ''
    },
    {
        bookName: '思考，好与坏',
        publisher: '重庆出版社',
        author: '杨念群',
        isbn: 9787020184262,
        borrowCount: 62,
        image: ''
    },
    {
        bookName: '思考，好与坏',
        publisher: '重庆出版社',
        author: '杨念群',
        isbn: 9787020184262,
        borrowCount: 62,
        image: ''
    },
]

const emit = defineEmits(['current-animation-finish'])
onMounted(() => {
    setTimeout(() => {
        emit('current-animation-finish')
    }, 3000)
})
</script>

<template>
    <div class="month-book-rank-page">
        <div class="title-section">
            <div class="title-box">
                2月借阅排行榜
            </div>
            <div class="subtitle-text">
                读者最喜欢借阅的图书
            </div>
        </div>
        <div class="books-section">
            <div class="book-box" v-for="(bookData, i) in monthBookRank" :key="`book${i}`">
                <div class="top-section">
                    <div class="rank-number">{{ i + 1 }}</div>
                    <div class="book-image-box">
                        <div class="book-image">
                            <BookCover />
                        </div>
                    </div>
                </div>
                <div class="bottom-section">
                    <div class="book-name">{{bookData.bookName}}</div>
                    <div class="publisher">出版社：{{bookData.publisher}}</div>
                    <div class="author">作者：{{bookData.author}}</div>
                    <div class="isbn">ISBN: {{ bookData.isbn }}</div>
                    <div class="checkouts">借阅次数：{{bookData.borrowCount}}次</div>
                </div>
            </div>
            
        </div>
    </div>
</template>

<style scoped lang="scss">
.month-book-rank-page {
    height: 1216px;
    background: #E7F2FF;
    padding: 70px;
}

.title-section {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 120px;
}

.title-box {
    height: 100px;
    background-color: #fff;
    border-radius: 50px;
    border: 4px solid #3692FF;
    padding: 10px 40px;
    color: #3692FF;
    font-size: 60px;
    line-height: 72px;
    font-weight: 500;
    box-shadow: 28px 15px #3692FF;
}

.subtitle-text {
    font-size: 64px;
    line-height: 93px;
    font-weight: 600;
    color: #3692FF;
}

.books-section {
    padding: 0 23px;
    display: flex;
}

.book-box {
    width: 430px;
    height: 730px;
    margin-right: 50px;
    border-radius: 30px;
    border: 4px solid #3692FF;
    background-color: #fff;
    padding: 0 55px;
    display: flex;
    flex-direction: column;

    .top-section {
        display: flex;
        justify-content: space-between;
        align-items: flex-end;
        height: 330px;
        padding-right: 16px;
        padding-bottom: 62px;
        border-bottom: 4px solid #3692FF;
        .rank-number {
            font-size: 96px;
            line-height: 100px;
            margin-bottom: -16px;
            color:#3692FF;
            font-weight: 600;
        }
        .book-image-box {
            margin-top: -35px;
            width: 224px;
            height: 300px;
            border: 3px solid #3692FF;
            border-radius: 20px;
            background-color: #fff;
            box-shadow: 16px 16px #C0DDFF;
        }
    }

    .bottom-section {
        padding: 50px 0;
        .book-name {
            font-size: 40px;
            line-height: 58px;
            font-weight: 700;
            color: #3692FF;
            margin-bottom: 20px;
            white-space: nowrap;
            max-width: 322px;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .publisher, .author, .isbn, .checkouts{
            font-size: 24px;
            line-height: 35px;
            color: #88BFFF;
            margin-bottom: 11.5px;
        }
    }
}

</style>