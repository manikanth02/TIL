### on Click of some email and Phone number How should we copied?

      const onCopy = (url:string,label:string) => {
        navigator.clipboard.writeText(url);
        snackbar(`${capitalize(label)} ID copied to clipboard`, "info");
      };

      onClick={()=> onCopy(email,"email")}

### How to onClick of icon we copy email,value and anything we want?
```
import ContentCopyIcon from "@mui/icons-material/ContentCopy";
import {IconButton} from "@mui/material";

 const onCopy = (url:string,label:string) => {
        navigator.clipboard.writeText(url);
        snackbar(`${capitalize(label)} ID copied to clipboard`, "info");
      };

<IconButton className="ml-2" onClick={() => onCopy(job.title, job.jobId)} size="small">
          <ContentCopyIcon fontSize="small" />
</IconButton >
```


