<template>
  <q-page class="row justify-center items-stretched q-pa-xl">
    <div class="col-8 bg-grey-3">
      {{ SelectedQuestion }}
      <br>
      <q-btn
        v-if="!videoRecording"
        label="record"
        @click="record"
        :disable="SelectedQuestion === undefined"
      />

      <q-btn
        v-else
        label="Stop"
        @click="StopRecord"
      />
    </div>
    <div class="col-4 bg-grey-2">
      <q-list
        bordered
        separator
      >
        <questionItem
          v-for=" (question,index) in questions_array"
          :key="index"
          :title="`Q${index+1}`"
          :question="question"
          :isSelected="(question === SelectedQuestion)"
          @SelectQuestion="selectQuestion"
          @DeleteBlob="DeleteBlob"
        />

      </q-list>
    </div>
  </q-page>
</template>

<script>
import questionItem from 'components/item.vue';
import { uid } from 'quasar';

export default {
  components: {
    questionItem,
  },
  name: 'PageIndex',
  data() {
    return {
      SelectedQuestion: undefined,
      videoRecording: false,
      questions_array: [
        {
          questionId: 1,
          questionContent: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit Nam ultricies augue urna?',
          videoBlob: undefined,

          deleted: false,
          videoSent: false,
        },
        {
          questionId: 2,
          questionContent: 'Morbi vehicula, magna eget volutpat viverra, dolor odio porta mi, placerat leo velit quis nisl?',
          videoBlob: undefined,
          deleted: false,
          videoSent: false,
        },
        {
          questionId: 3,
          questionContent: 'Quisque facilisis ullamcorper hendrerit. Pellentesque lobortis?',
          videoBlob: undefined,
          deleted: false,
          videoSent: false,
        },
        {
          questionId: 4,
          questionContent: 'odio in est luctus, et vulputate enim ornare. Duis nec diam ultrices, mattis velit eu?',
          videoBlob: undefined,
          deleted: false,
          videoSent: false,
        },
        {
          questionId: 5,
          questionContent: 'blandit mauris. Duis euismod lorem quis elementum posuere?',
          videoBlob: undefined,
          deleted: false,
          videoSent: false,
        },
      ],

    };
  },
  created() {
    this.MoveToNextQuestion();
  },
  methods: {
    selectQuestion(question) {
      this.SelectedQuestion = question;
    },
    DeleteBlob(question) {
      question.videoBlob = undefined;
    },
    record() {
      this.videoRecording = true;
    },
    StopRecord() {
      this.videoRecording = false;
      this.SelectedQuestion.videoBlob = uid();
      this.MoveToNextQuestion();
    },
    MoveToNextQuestion() {
      this.SelectedQuestion = this.questions_array.find(
        (question) => question.videoBlob === undefined,
      );
    },
  },
};
</script>
