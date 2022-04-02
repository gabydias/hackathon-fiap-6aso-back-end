# teste
  - name: Deploy Backend no  Cloud Run
        id: deploy
        run: |-
          gcloud run deploy backend \
            --quiet \
            --region  ${{ secrets.GOOGLE_REGION }} \
            --image ${{ secrets.ARTIFACT_REGISTRY }}/backend:latest \
            --platform managed \
            --set-env-vars CLOUD_SQL_CONNECTION_NAME=${{ secrets.CLOUD_SQL_CONNECTION_NAME }},CLOUD_SQL_DATABASE_NAME=${{ secrets.CLOUD_SQL_DATABASE_NAME }},CLOUD_SQL_PASSWORD=${{ secrets.CLOUD_SQL_PASSWORD }},CLOUD_SQL_USERNAME=${{ secrets.CLOUD_SQL_USERNAME }} \
            --allow-unauthenticated \
            --add-cloudsql-instances ${{ secrets.CLOUD_SQL_CONNECTION_NAME }} \
            --project ${{ secrets.GOOGLE_PROJECT_ID }} \
            --format json
