 ### How should we Apply Delete Functionality??

Note :   Always keeps warning Dialogue Box on Delete becaues it may be posible he click/tap by mistake


Approach: 
1.We maintain a state to activate dialogue Box,and a variable to store _id.

```

import "./index.scss";
import { Button, Dialog, DialogTitle, DialogContent, DialogContentText, DialogActions } from "@mui/material";
import { FC, MouseEvent } from "react";
interface props {
    isOpen: boolean;
    title: string;
    description: string;
    onClose: (e: MouseEvent<HTMLElement>) => void;
    onConfirm: (e: MouseEvent<HTMLElement>) => void;
}

const WarningDialog: FC<props> = ({ isOpen, title, description, onClose, onConfirm }) => (
    <Dialog
        open={isOpen}
        onClose={onClose}
        aria-labelledby="alert-dialog-title"
        aria-describedby="alert-dialog-description"
        className="custom-dialog-root"
    >
        <DialogTitle id="alert-dialog-title">
            {title}
        </DialogTitle>
        <DialogContent>
            <DialogContentText id="alert-dialog-description">
                {description}
            </DialogContentText>
        </DialogContent>
        <DialogActions>
            <Button variant='outlined' onClick={onClose}>Cancel</Button>
            <Button onClick={onConfirm} autoFocus>
                Confirm
            </Button>
        </DialogActions>
    </Dialog>
);

export default WarningDialog;

```


### styling 

```
/* Custom styles for the custom dialog */
.custom-dialog-root {
  & .MuiDialog-paper {
    width: 500px;
    height: 160px;
    max-width: 600px;
    max-height: calc(100% - 64px);
  }

  /* Custom styles for the DialogTitle */
  & .MuiDialogTitle-root {
    padding: 16px 24px;
  }

  /* Custom styles for the DialogContent */
  & .MuiDialogContent-root {
    padding: 8px 24px;
  }
}

```
```

const [state,setState] = useState({
deleteWarning:false;
_deleteId:"";
});

```

### This creates delete Icon in every row

```

  const createRows = (project:IProject,index:number) => {
        const action = <GetActions
        icons={[
            {
                name: "Edit", method: () =>
                   { 
                    setOpenState(true);
                    navigate({
                        pathname:"" + project._id,
                        search:searchParams.toString()
                    });},

            },
            { name: "Delete", method: () => handleDelete(project._id)},
        ]}
    />;
        return{
            id:1,
            name:project?.name,
            action
        };
    };

let rows:IProjectRows[] = [];
    if(projectsList?.data?.data.length){
         rows = projectsList?.data?.data.map((project:IProject,index:number) => createRows(project,index));
    }

```


### Calling Delete Warnng Component

```

<WarningDialog 
            isOpen={state.deleteWarning}
            onClose={() => handleDelete}
            onConfirm={onDelete}
            title="Delete Project"
            description="You can't undo this action"

            />

```

### handleDelete() Which Activate(open) dialogue Box


```

const handleDelete = (_deleteId="") => {
        setState((prevState) => ({
            ...prevState,
            deleteWarning : !prevState.deleteWarning,
            _deleteId:_deleteId
        }));
    };

```

### on CONFIRM button we integrate delete API

```

const onDelete = async () => {
        try{
          const response = await deleteContentProject({_id:state._deleteId});
          navigate("/content/products");
          snackbar(response?.message,"success");
          handleDelete();
        }catch(error){
            const err = error as IErrorResponse;
            console.log("Error in Add Projects",err);
            snackbar(err?.data?.message,"error");
        }
    };

```

### How to write Delete API

```

 const deleteContentProject = async(query:object):Promise<IProjectProductResponse> =>
    new Promise((resolve,reject) => {
      httpRequest<IProjectProductResponse>("DELETE",`${product}`,{},query)
      .then(resolve)
      .catch(reject);
    });

```
